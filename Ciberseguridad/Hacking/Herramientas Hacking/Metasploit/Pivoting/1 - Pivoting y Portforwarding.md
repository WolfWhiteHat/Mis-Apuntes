
Para hacer pivoting desde metasploit primero necesitaremos obtener acceso a la primera maquina

Estas son las dos maquinas que hay, nosotros solo tenemos acceso a la primera maquina
![[Pasted image 20240409122710.png]]

Aqui podemos ver que ya tenemos acceso y vemos en la red en la que esta conectado
![[Pasted image 20240409123819.png]]
![[Pasted image 20240409124006.png]]
![[Pasted image 20240409131256.png]]

Ahora ejecutaremos el siguiente comando para agregar una ruta a toda la red
```Bash
run autorute -s 10.2.18.0/20
```
![[Pasted image 20240409125808.png]]

Una vez tenemos toda la ruta agregada ahora desde metasploit podremos ejecutar modulos sobre la segunda maquina victima, para ello ejecutaremos un modulo para ver que puertos tiene abiertos
![[Pasted image 20240409130124.png]]

Una vez vemos que ya hemos podido ver los puertos de la maquina, ahora desde la sesion que ya tenemos abierta de meterpreter realizaremos portforwarding del puerto 80 para redirigirlo a un puerto de nuestra maquina local
![[Pasted image 20240409130514.png]]

Ahora sin cerrar la consola ejecutaremos nmap para escanear el puerto 80 de la maquina victima 2, para ello el escaneo apuntara a nuestro puerto 1234
![[Pasted image 20240409130752.png]]

Una vez visto el servicio a explotar lo configuraremos y lo ejecutaremos, como podemos ver ya hemos obtenido acceso a la segunda maquina y tenemos las dos sesiones de meterpreter abiertas
![[Pasted image 20240409131055.png]]
![[Pasted image 20240409131152.png]]
![[Pasted image 20240409131216.png]]



