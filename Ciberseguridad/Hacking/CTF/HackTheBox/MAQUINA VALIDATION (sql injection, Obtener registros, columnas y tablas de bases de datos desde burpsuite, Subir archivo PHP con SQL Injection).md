Cómo siempre es saber si estamos ante un linux o un windows, donde veremos que se trata de un linux al ver el TTL:
![[Mis apuntes/ANEXOS/Pasted image 20230421024534.png]]
Ahora escaneamos los puertos abiertos:
![[Mis apuntes/ANEXOS/Pasted image 20230421024542.png]]
Y ahora inspeccionamos esos puertos abiertos, donde vemos que hay varios servidores web pero que dan error, excepto el puerto 80 que es el que está funcionando:
![[Mis apuntes/ANEXOS/Pasted image 20230421024551.png]]
Y por último inspeccionamos el servidor web que tiene esta máquina con whatweb:
![[Mis apuntes/ANEXOS/Pasted image 20230421024601.png]]
Si entramos en el servidor web de la máquina vemos esto:
![[Mis apuntes/ANEXOS/Pasted image 20230421024608.png]]
Si ponemos un usuario, vemos que se nos repite:
![[Mis apuntes/ANEXOS/Pasted image 20230421024618.png]]
Por tanto vamos a probar a ver si es vulnerable a html injection:
![[Mis apuntes/ANEXOS/Pasted image 20230421024625.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230421024630.png]]
Ahora vamos a interceptar con burp suite la petición y vamos a hacer una sql injection, donde vamos a listar las bases de datos disponibles con union select:
![[Mis apuntes/ANEXOS/Pasted image 20230421024638.png]]
Y ya lo tenemos:
![[Mis apuntes/ANEXOS/Pasted image 20230421024646.png]]
Ahora vamos a buscar otras bases de datos disponibles aparte de la actual, para ello lo haremos así:
![[Mis apuntes/ANEXOS/Pasted image 20230421024654.png]]
Y se nos muestran otras bases de datos:
![[Mis apuntes/ANEXOS/Pasted image 20230421024701.png]]
Ahora vamos a enumerar las tablas de la base de datos registration:
![[Mis apuntes/ANEXOS/Pasted image 20230421024709.png]]
Y una vez hecho esto podemos ver como la tabla se llama registration:
![[Mis apuntes/ANEXOS/Pasted image 20230421024716.png]]
Ahora vamos a enumerar las columnas de la tabla registration:
![[Mis apuntes/ANEXOS/Pasted image 20230421024723.png]]
Y este es el resultado:
![[Mis apuntes/ANEXOS/Pasted image 20230421024729.png]]
Ahora vamos a enumerar los registros por ejemplo de username y userhash:
![[Mis apuntes/ANEXOS/Pasted image 20230421024737.png]]
Y nos sale esta información, la cual vamos a guardar por si acaso:
![[Mis apuntes/ANEXOS/Pasted image 20230421024744.png]]
Ahora vamos a ver cómo insertar un archivo de texto dentro de la máquina a través de una sql injection:
![[Mis apuntes/ANEXOS/Pasted image 20230421024754.png]]
Y ahora si ponemos el nombre del fichero que hemos inyectado en el navegador, veremos cómo podemos acceder a él:
![[Mis apuntes/ANEXOS/Pasted image 20230421024800.png]]
Ahora vamos a insertar código en php que nos sirva para ejecutar comandos en esta máquina remota:
![[Mis apuntes/ANEXOS/Pasted image 20230421024807.png]]
Y ya me cargó una página php preparada para ejecutar comandos:
![[Mis apuntes/ANEXOS/Pasted image 20230421024814.png]]
Por ejemplo un whoami:
![[Mis apuntes/ANEXOS/Pasted image 20230421024827.png]]
Ahora que podemos ejecutar comandos, podemos ejecutar el comando que nos permitía conseguir una reverse shell, por tanto en condiciones normales ejecutaríamos este comando:
![[Mis apuntes/ANEXOS/Pasted image 20230421024837.png]]
Y ahora si pegamos esta parte codificada como URL en el navegador en la parte del cmd, mientras estamos escuchando por ejemplo por el puerto 443, conseguiremos la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230421024845.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230421024847.png]]
Lo pegamos:
![[Mis apuntes/ANEXOS/Pasted image 20230421024855.png]]
Y recibimos la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230421024902.png]]
Y navegando por los directorios, obtenemos la flag:
![[Mis apuntes/ANEXOS/Pasted image 20230421024910.png]]
Dentro del directorio /var/www/html vemos que hay un archivo llamado config.php donde se nos muestran unas credenciales:
![[Mis apuntes/ANEXOS/Pasted image 20230421024916.png]]
Pegamos esta contraseña al loguearnos como root y vemos que es correcta y ya somos usuarios root:
![[Mis apuntes/ANEXOS/Pasted image 20230421024923.png]]
Nos ubicamos dentro del directorio root y vemos que accedemos a la flag de root:
![[Mis apuntes/ANEXOS/Pasted image 20230421024930.png]]
