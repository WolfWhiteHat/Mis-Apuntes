Mimikatz es una herramienta posterior a la explotación utilizada por los atacantes **para extraer credenciales confidenciales, como contraseñas y hashes, de un sistema operativo Windows**

Para comenzar primero realizaremos un escaneo de nmap
![[Pasted image 20240312072124.png]]

Vamos a buscar si hay algun exploit para poder utilizar
![[Pasted image 20240312072211.png]]

Como vemos tenemos exploit para la versión que tiene la maquina victima, para ello arrancamos metasploit y cargamos el exploit
![[Pasted image 20240312072322.png]]

Configuramos el exploit y lo ejecutamos para obtener una sesión de meterpreter
![[Pasted image 20240312072426.png]]

Migramos la sesión
![[Pasted image 20240312073119.png]]

Ejecutamos kiwi
![[Pasted image 20240312073050.png]]

Una vez iniciado kiwi escribimos el siguiente comando para ver el valor hash NTLM del usuario administrador
creds_all
![[Pasted image 20240312073512.png]]

Ahora con el siguiente comando sacaremos el valor hash de todos los usuarios
lsa_dump_sam
![[Pasted image 20240312073612.png]]
