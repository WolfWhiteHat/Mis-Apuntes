Realizamos un escaneo con nmap
![[Pasted image 20240605131912.png|1500]]

Comenzamos haciendo un ataque de fuerza bruta a la web
![[Pasted image 20240605133218.png]]

Encontramos un directorio, lo abrimos y encontramos el servicio `pluck 4.7.13`
![[Pasted image 20240605133323.png]]


Encontramos un exploit en la base de datos de exploitdb, este exploit nos permite subir archivos para ejecutar codigo de forma remota
https://www.exploit-db.com/exploits/49909
![[Pasted image 20240605133510.png]]

Antes de poder ejecutar el exploit necesitaremos obtener la password, revisamos por internet y probamos con la contraseña por defecto y como vemos hemos podido acceder, la contraseña es `password`
![[Pasted image 20240605141346.png]]

Ahora si ejecutaremos el exploit
```Bash
python3 exploit.py 10.10.167.255 password /app/pluck-4.7.13
```
![[Pasted image 20240605141839.png]]

Copiamos la url y la pegamos en el navegador, ahora tendremos acceso a una shell de la maquina victima
![[Pasted image 20240605142000.png]]

Ahora generaremos una reverse shell estable
![[Pasted image 20240605144256.png]]


## Escalada de privilegios de data a lucien

Ahora vamos a realizar la escalada de privilegios de todos los usuarios del sistema
![[Pasted image 20240606084434.png]]

Primero buscamos los binarios que podemos ejecutar con el usuario actual
![[Pasted image 20240606084407.png]]

Seguido también revisamos todos los ficheros .py que se pueden ejecutar y encontramos dos en la carpeta `/opt`
![[Pasted image 20240606084325.png]]
![[Pasted image 20240606084659.png]]

Leemos el primer fichero y obtenemos unas credenciales
![[Pasted image 20240606084811.png]]

Y este es el contenido del segundo script
![[Pasted image 20240606085049.png]]

Probamos con las credenciales del usuario Lucien y hemos obtenido acceso al usuario
![[Pasted image 20240606085446.png]]
![[Pasted image 20240606085621.png]]

## Escalada de privilegios de lucien a death
Una vez obtenido el acceso al usuario de lucien revisamos que puede ejecutar como root y encontramos que podemos ejecutar el archivo `getDreams.py` el cual conecta a la base de datos con el usuario death
![[Pasted image 20240606085833.png]]

En la carpeta de lucien leemos los ficheros del historia de bash y de mysql para revisar los comandos ejecutados
![[Pasted image 20240606090542.png]]
![[Pasted image 20240606090629.png]]

Nos encontramos que tenemos dos ficheros con el mismo nombre en diferentes ubicaciones, en la ubicación de death encontramos que solo podemos ejecutarlo y nos muestra un listado de una tabla de la base de datos
![[Pasted image 20240606091015.png]]

Revisamos otra vez el fichero getDreams.py de la ubicación /opt
![[Pasted image 20240606091228.png]]

En el fichero de `.bash_history` encontramos las credenciales de la base de datos de lucien
![[Pasted image 20240606092231.png]]

Probamos a acceder y ya estamos dentro de la base de datos
![[Pasted image 20240606092004.png]]

Revisamos la base de datos y encontramos la tabla la cual muestra el archivo .py visto anteriormente
![[Pasted image 20240606094155.png]]

Aqui la comprobación
![[Pasted image 20240606094221.png]]
![[Pasted image 20240606091015.png]]

Continuaremos realizando el ataque por aqui, revisamos cual es la estructura de esta libreria la cual podemos verla en el fichero getDreams.py del fichero /opt
![[Pasted image 20240606094458.png]]

Añadiremos un valor a la tabla de dreams
![[Pasted image 20240606094940.png]]

Ahora al ejecutar con el usuario death el archivo getDreams.py el cual solo tenemos acceso de ejecucion y habiendo añadido previamente el comando nos listara todo el contenido del fichero `/home/death/getDreams.py` y encontramos la password de death
![[Pasted image 20240606095224.png]]

Probamos ha acceder y ya habremos obtenido el acceso con el usuario death
![[Pasted image 20240606095904.png]]

## Escalada de privilegios de death a morpheus
Ejecutamos el siguiente comando para revisar que porgramas podemos ejecutar y a que tenemos permisos y encontramos un arhivo de python el cual tenemos acceso
```Bash
find / -group death -type f 2>/dev/null
```
![[Pasted image 20240606114903.png]]
![[Pasted image 20240606114311.png]]

Ahora cambiaremos el contenido del fichero por nuestro payload, para ello primero vaciamos el fichero
```Bash
echo "" > /usr/lib/python3.8/shutil.py
```
![[Pasted image 20240606115410.png]]

Añadimos nuestro payload
![[Pasted image 20240606115541.png]]

Nos ponemos en escucha con netcat
![[Pasted image 20240606115631.png]]

Y ahora solo falta esperar a obtener la reverse shell
![[Pasted image 20240606121622.png]]

Con la herramienta pspy hemos podido ver que el archivo shutil.py estaba en una tarea y al poder modificarlo y añadir nuestro paylaod una vez modificado al ejecutar la tarea obtenemos la sesion bash
![[Pasted image 20240606124057.png]]
