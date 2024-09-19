Vamos a recopilar información para preparar un ataque al puerto 25 de la maquina metasploitable

Para ellos probaremos un par de escaner que tenemos en metasploit
Con los dos siguiente escaneos ya tenemos algo mas de información sobre el puerto y servicio a explotar
![[Pasted image 20240206132037.png|1500]]
![[Pasted image 20240206132314.png]]


Con el comando nc (netcat) estamos a la escuchar del puerto 25 ya que queremos explotar la vulnerabilidad del protocolo SMTP, el comando VRFY lo utilizamos para verificar usuarios, con el obtendremos la respuesta si el usuario que estamos solicitando existe o no.
![[Pasted image 20240206134218.png]]


A continuación instalaremos y ejecutaremos la herramienta smpt-users-enum, este programa automatiza el proceso de VRFY para encontrar todos los usuarios que haya en el servidor
![[Pasted image 20240206134533.png]]

smtp-user-enum -M VRFY -U /usr/share/wordlists/fern-wifi/common.txt -t 192.168.60.3
![[Pasted image 20240206143213.png]]
