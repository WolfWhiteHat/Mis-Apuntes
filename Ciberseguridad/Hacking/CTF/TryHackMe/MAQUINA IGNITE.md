Hacemos el escaneo con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230910110754.png]]

Y esta es la web:
![[Pasted image 20231103153039.png]]

Y en la parte de abajo de esta web vemos que hay unas credenciales por defecto dentro del directorio /fuel:
![[Pasted image 20231103153356.png]]

Y tenemos un panel de login, donde probamos con admin:admin:
![[Pasted image 20231103153459.png]]

Donde tenemos el siguiente entorno:
![[Pasted image 20231103153532.png]]

Hacemos fuzzing web y encontramos el directorio assets:
![[Pasted image 20240529095151.png]]

Nos damos cuenta que podemos subir ficheros, comoprimimos la reverse_shell de php y al subirlo seleccionamos que lo descomprima, como podemos ver ya lo tenemos subido
Ahora nos ponemos en escucha con netcat y al ejecutarlo en el servidor obtenemos acceso a la maquina victima
![[Pasted image 20240529095321.png]]

Ya tenemos acceso a la terminal de la maquina, ahora buscaremos obtener privilegios de root, para ello primero buscaremos las credenciales, anteriormente hemos visto que en la web indicaba un fichero para la instalación de la base de datos
![[Pasted image 20240529100302.png]]

Buscamos el fichero y lo leemos, al abrirlo obtenemos las credenciales de root
![[Pasted image 20240529100359.png]]

Intentamos acceder al usuario root pero nos salta un error porque estamos con una sesión de shell basica, para poder obtener acceso de root primero ejecutaremos el siguiente comando para obtener una /bin/bash
```Bash
python -c 'import pty; pty.spawn("/bin/bash")'
```
![[Pasted image 20240529100655.png]]

Y como podemos ver ahora si nos deja acceder como root
![[Pasted image 20240529101004.png]]

Y ya podriamos obener la flag de root
![[Pasted image 20240529101159.png]]


