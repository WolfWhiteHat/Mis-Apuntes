
Vamos a encontrar el hash del usuario root, para ello primero escanearemos el host victima
nmap -sV 192.130.196.3
![[Pasted image 20240314142714.png]]

Como vemos en la siguiente captura tiene el puerto 21 abierto
nmap -sV -p 21 --script vuln -T5 192.130.196.3
![[Pasted image 20240314143051.png]]

Buscamos algun exploit para poder acceder a la maquina victima
searchsploit prodtpd
![[Pasted image 20240314143024.png]]

Ya tenemos acceso a la maquina victima
![[Pasted image 20240314143255.png]]
![[Pasted image 20240314143255.png]]

Ahora configuraremos y ejecutaremos el siguiente modulo para obtener el hash
post/linux/gather/hashdump
![[Pasted image 20240314143436.png]]


Ahora utilizaremos el siguiente modulo para poder sacar la contraseña del has, para ello seleccionamos el modulo y lo configuramos
![[Pasted image 20240314144322.png]]


Lo ejecutamos y ya obtendríamos las credenciales
![[Pasted image 20240314144354.png]]


