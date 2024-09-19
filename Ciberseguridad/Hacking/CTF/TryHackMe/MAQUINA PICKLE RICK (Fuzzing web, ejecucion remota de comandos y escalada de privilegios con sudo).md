Hacemos un escaneo de nmap y encontramos el puerto 22 y 80 abiertos
![[Pasted image 20240625140433.png]]

Al acceder a la web encontramos la siguiente pagina
![[Pasted image 20240625140523.png]]

Al revisar el codigo encontramos un posible usuario
![[Pasted image 20240625140559.png]]

Hacemos fuzzing web y encontramos los siguientes directorios
![[Pasted image 20240625142913.png]]

Revisamos el fichero de robots.txt y encontramos una posible contraseña
![[Pasted image 20240625142347.png]]

Si vamos a la carpeta de assstes encontramos una foto con el nombre de portal.jpg, esta imagen no esta en la pagina principal, probamos a buscar y encontramos un portal
```
R1ckRul3s
Wubbalubbadubdub
```
![[Pasted image 20240625143215.png]]

Probamos con el usuario y la password que hemos encontrado y obtenemos acceso, al entrar tenemos un panel para ejecutar comandos dentro del ordenador
![[Pasted image 20240625143555.png]]

Nos ponemos en escucha con netcat y nos generamos una reverse shell
![[Pasted image 20240625143836.png]]

Y ya tendríamos acceso a la maquina victima
![[Pasted image 20240625143857.png]]

Nos generamos una TTY estable y obtenemos la primera flag
![[Pasted image 20240625144309.png]]

Vamos al directorio de rick y encontramos la segunda flag
![[Pasted image 20240625144342.png]]

Ahora vamos a escalar los privilegios a root, para ello revisamos que podemos ejecutar como root y encontramos que podemos ejecutar todos los comandos
![[Pasted image 20240625144438.png]]

Asi que unicamente nos logueamos como root y ya podriamos obtener la ultima flag
![[Pasted image 20240625144525.png]]
![[Pasted image 20240625144553.png]]

