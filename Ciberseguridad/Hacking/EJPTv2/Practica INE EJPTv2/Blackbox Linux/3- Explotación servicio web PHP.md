
Primero realizamos un escaneo del servidor instalado en el puerto 80
```
nmap -sV -sC -p80 
```
![[Pasted image 20240501114155.png]]

Revisamos el archivo `phpinfo.php` el cual suele obtener bastante información
![[Pasted image 20240501114418.png]]

Buscamos un exploit para atacar el servicio
```
searchsploit php cgi
```
![[Pasted image 20240501114555.png]]

Nos descargamos el exploit
```
searchsploit -m 18836.py
```
![[Pasted image 20240501114734.png]]

Si ejecutamos directamente el exploit sin configurarlo nos mostrara información del servicio
![[Pasted image 20240501115048.png]]

Ahora lo configuramos para obtener una reverse shell
![[Pasted image 20240501115841.png]]

Ahora desde otra terminal nos ponemos a escuchar con netcat
```
nc -nvlp 1234
```
![[Pasted image 20240501115705.png]]

Ejecutamos el exploit
![[Pasted image 20240501115926.png]]

Y como podemos ver desde la termianl con el oyente de netcat obtenemos acceso al sistema con el usuario www
![[Pasted image 20240501120010.png]]

Esto podemos automatizarlo desde metasploit con el siguiente modulo
`exploit/multi/http/php_cgi_arg_injection`
![[Pasted image 20240501120136.png]]

Seleccionamos el exploit, lo configuramos y lo ejecutamos, como podemos ver en las siguientes capturas hemos obtenido acceso con el mismo usuario
![[Pasted image 20240501120335.png]]
![[Pasted image 20240501120353.png]]

