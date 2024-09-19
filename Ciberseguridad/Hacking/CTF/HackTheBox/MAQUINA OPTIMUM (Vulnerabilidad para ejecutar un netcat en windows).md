Lo primero será hacer los reconocimientos de siempre:
![[Mis apuntes/ANEXOS/Pasted image 20230410101737.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230410101741.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230410101744.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230410101750.png]]
Vemos que el servicio que corre por el puerto 80 es un httpfileserver (que sirve para compartir archivos) que está sobre un apache en una versión antigua, por lo que podemos buscar exploits para esta versión, aunque también podemos buscarlo por el nombre abreviado y nos encuentra más:
![[Mis apuntes/ANEXOS/Pasted image 20230410101811.png]]
Nos bajamos uno de ellos, el penúltimo:
![[Mis apuntes/ANEXOS/Pasted image 20230410101820.png]]
Y si entramos dentro del exploit, estas son las instrucciones, donde nos dicen que debemos montar un servidor netcat y ejecutarlo varias veces:
![[Mis apuntes/ANEXOS/Pasted image 20230410101828.png]]
Ahora vamos a modificar la parte donde se recogen las direcciones IP y el puerto, donde debemos de poner lo nuestro:
![[Mis apuntes/ANEXOS/Pasted image 20230410101838.png]]
En este punto vamos a montar un servidor web con python para ofrecer el netcat a la máquina víctima, por tanto primero vamos a descargar netcat para windows:
![[Mis apuntes/ANEXOS/Pasted image 20230410101847.png]]
Ahora lo descargamos y lo descomprimimos creando una nueva carpeta que se llame netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230410101855.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230410101900.png]]
Ahora montamos el servidor web:
![[Mis apuntes/ANEXOS/Pasted image 20230410101908.png]]
Ahora nos ponemos a escucha con netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230410101917.png]]
Y es momento de lanzar el exploit:
![[Mis apuntes/ANEXOS/Pasted image 20230410101930.png]]
Y ahora con netcat habremos recibido la shell reversa:
![[Mis apuntes/ANEXOS/Pasted image 20230410101940.png]]