Primero realizamos un escaneo del servicio de mysql y añadimos uno de los servidores web alojados porque una vez explotados la base de datos obtendremos acceso a las aplicaciones web
```
nmap -sV -sC -p3306,8585 10.2.31.244
```
![[Pasted image 20240425193321.png]]

Revisamos los exploits que tiene esta versión de MySQL
![[Pasted image 20240425193607.png]]

No vemos nada interesante, así que realizaremos un ataque de fuerza bruta desde metasploit
![[Pasted image 20240425194126.png]]
![[Pasted image 20240425194258.png]]
![[Pasted image 20240425195029.png]]

Como podemos ver tiene una configuración muy mala porque el usuario root no tiene contraseña, asi que accederemos con el siguiente comando
```
mysql -u root -p -h 10.2.26.57
```
![[Pasted image 20240425195237.png]]

También habíamos revisado que tenemos una web de WAMP instalada en el puerto 8585 en la cual vemos que hay un wordpres instalado
![[Pasted image 20240425195836.png]]

Si intententamos acceder al archivo phpmyadmin que es donde se almacenan las contraseñas veremos que no tenemos acceso para modificarlo
![[Pasted image 20240425195929.png]]

Anteriormente hemos detectado la vulnerabilidad de eternalblue que nos daba permisos de administrador en el servidor para poder llegar a este archivo, es necesario entrar con los privilegios mas altos, asi que accederemos desde esta vulnerabilidad para manipular el archivo
![[Pasted image 20240425200214.png]]

Una vez obtenido el acceso con los privilegios buscaremos el archivo wp-config.php donde se alojan los usuarios y las contraseñas de la base de datos de mysql
![[Pasted image 20240425200401.png]]
![[Pasted image 20240425200429.png]]
![[Pasted image 20240425200502.png]]
![[Pasted image 20240425201312.png]]

Una vez encontrado el archivo wp-config.php si lo leemos podremos ver los usuarios, en este vemos el usuario root sin contraseña
![[Pasted image 20240425201544.png]]
![[Pasted image 20240425201452.png]]

Ahora buscaremos el archivo phpmyadmin para descargarlo y modificarlo ya que es el encargado del control de acceso, lo descargamos y lo editamos
![[Pasted image 20240425202001.png]]

Aqui tenemos el archivo ya descargado
![[Pasted image 20240425202128.png]]

Entramos en el archivo y lo siguiente que esta marcado son los permisos los cuales pueden acceder los usuarios
![[Pasted image 20240425202337.png]]

Lo modificamos para poder acceder
![[Pasted image 20240425202426.png]]

Y resubimos el archivo modificado
![[Pasted image 20240425202547.png]]

Confirmamos que esten los cambio aplicados
![[Pasted image 20240425202640.png]]

Si ahora volvemos a acceder desde el navegador puede parecer que no se han aplicado los cambios, eso es porque es necesario reiniciar el servicio de apache, para ello ejecutaremos el siguiente comando en una terminal shell de la maquina
![[Pasted image 20240425202945.png]]
![[Pasted image 20240425203135.png]]

Si ahora volvemos a probar podemos ver que hemos obtenido el acceso
![[Pasted image 20240425203202.png]]

Todo esto lo hemos realizado para modificar la contraseña del usuario admin desde un servidor web
![[Pasted image 20240425203346.png]]

Modificamos la password del usuario admin
![[Pasted image 20240425203621.png]]

Ahora podremos acceder a la web de wordpress
![[Pasted image 20240425203858.png]]
![[Pasted image 20240425203915.png]]
![[Pasted image 20240425203939.png]]




