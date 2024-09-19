Realizamos un escaneo del sistema
```
nmap -sV -p1-10000 10.2.31.11
```
![[Pasted image 20240429081105.png]]

Revisamos los puertors abiertos y detectamos el 512 y 513, intentamos hacer una shell con netcat y obtenemos acceso, esom significa que estaba configurado el puerto como oyente
![[Pasted image 20240429081330.png]]

Comprobación usuario con el que hemos accedido
![[Pasted image 20240429081307.png]]

Revisamos los usuarios que hay en el sistema accediendo a la carpeta home
![[Pasted image 20240429081412.png]]


Revisamos la configuración de WebDav
![[Pasted image 20240429081528.png]]

