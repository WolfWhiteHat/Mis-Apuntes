
Primero realizamos un escaneo del host basico
nmap 10.2.29.88
![[Pasted image 20240307130932.png]]

Realizamos un escaneo mas preciso sobre el puerto que queremos explotar

nmap -sV -p 80 --script http-enum
![[Pasted image 20240307131243.png]]


Ejecutamos la herramienta davtest -url http://10.2.29.88/webdav
![[Pasted image 20240307131513.png]]

Ahora que hemos visto que podemos cargar archivos vamos a ejecutar la herramienta de metasploit y a ejecutaremos el sigueinte exploit
exploit/windows/iis/iis_webdav_upload_asp
![[Pasted image 20240307131943.png]]

Ejecutamos el comando y como podemos ver hemos accedido al sistema, como se puede ver en la imagen el proceso que realiza es el siguiente.
Comienza lanzando un comando de escucha en nuestro host por el puerto 4444
Genera un exploit que carga en la maquina victima
Lo ejecuta y después lo elimina para no dejar rastro
Una vez de ha ejecutado nuestra maquina oyente se conecta con una sesion de meterpreter
![[Pasted image 20240307132118.png]]


Una vez dentro iniciamos un shell y buscamos la bandera
![[Pasted image 20240307132516.png]]
