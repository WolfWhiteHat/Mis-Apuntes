Primero analizamos los puertos abiertos de la maquina victima
![[Pasted image 20240308081457.png]]

Una vez visto el puerto atacar prepararemos el ataque, en este caso accederemos por el protocolo 445 que es el servicio SMB, para ello utilizaremos la herramienta psexec, pero antes necesitaremos las credenciales del equipo. Realizaremos un ataque de fuerza bruta con metasploit

Ejecutamos metasploit y postgresql
service postgresql start && msfconsole
![[Pasted image 20240308081653.png]]

Para realizar la fuerza bruta utilizaremos el siguiente auxiliar
scanner/smb/smb_login
![[Pasted image 20240308081748.png]]


Como es un ataque de fuerza bruta tendremos que especificar un diccionario de usuario y contraseñas.

La configuracion sera la siguiente
Indicaremos la ip victima, un diccionario para los usuarios y otro para las contraseñas y configurando VERBOSE false especificamos que solo nos muestre en pantalla cuando encuentre algun usuario y contraseña.
![[Pasted image 20240308082056.png]]
![[Pasted image 20240308082250.png]]

Lanzamos el exploit y nos mostrara las contraseñas que vaya descubriendo
![[Pasted image 20240308082911.png]]


Una vez obtenidas las credenciales ahora ejecutaremos el siguiente exploit
exploit/windows/smb/psexec
![[Pasted image 20240308083815.png]]

Y como podemos ver tenemos acceso con el usuario administrador que especifica que tenemos los privilegios mas altos



