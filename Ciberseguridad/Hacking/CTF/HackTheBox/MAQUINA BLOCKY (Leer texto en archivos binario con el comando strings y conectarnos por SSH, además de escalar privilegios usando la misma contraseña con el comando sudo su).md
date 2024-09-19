Lo primero será hacer el reconocimiento de siempre, donde veremos que se trata de una máquina Linux y tiene abierto el puerto ftp, ssh, el puerto 80 y el de MInecraft:
![[Mis apuntes/ANEXOS/Pasted image 20230312011919.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230312012108.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230312012113.png]]
Siempre que veamos abierto un puerto ftp hay que probar en loguearnos como anonymous, aunque no ha funcionado:
![[Mis apuntes/ANEXOS/Pasted image 20230312012127.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230312012131.png]]
Ahora que vemos que hay una página web, vamos a entrar con el navegador, aunque si nos da problemas para acceder, tendremos que marcarla en el etc/hosts:
![[Mis apuntes/ANEXOS/Pasted image 20230312012145.png]]
Accedemos a la web:
![[Mis apuntes/ANEXOS/Pasted image 20230312012158.png]]
Ahora vamos a hacer un pequeño escaneo por los directorios de la web; esto hará algo parecido a gobuster pero con un mini diccionario, se trata de un ataque pequeño y rápido:
![[Mis apuntes/ANEXOS/Pasted image 20230312012210.png]]
Vamos a entrar en el phpMyAdmin:
![[Mis apuntes/ANEXOS/Pasted image 20230312012218.png]]
Ahora vamos a hacer lo mismo pero con wfuzz, excluyendo los mensajes de error 404 de esta manera:
![[Mis apuntes/ANEXOS/Pasted image 20230312012229.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230312012233.png]]
Vemos que hay un directorio llamado plugins, lo cual es raro, vamos a entrar en él y vemos que tenemos acceso a dos archivos:
![[Mis apuntes/ANEXOS/Pasted image 20230312012243.png]]
Descargamos por ejemplo el primero, blockycore y vamos a examinarlo, por tanto vamos a descomprimir el archivo:
![[Mis apuntes/ANEXOS/Pasted image 20230312012254.png]]
Y ahora al descomprimirse no vemos nada, pero si ejecutamos el comando tree -fas veremos los archivos por jerarquía:
![[Mis apuntes/ANEXOS/Pasted image 20230312013526.png]]
El archivo del medio parece que es el que puede tener más información, pero es un fichero binario, por tanto para leerlo podemos hacerlo con el comando strings:
![[Mis apuntes/ANEXOS/Pasted image 20230312012319.png]]
Y este es el resultado del interior de este fichero, donde parece que tenemos un usuario y contraseña, la cual es root:8YsqfCTnvxAUeduzjNSXe22:
![[Mis apuntes/ANEXOS/Pasted image 20230312012331.png]]
Vamos a probar ese usuario root y la contraseña en el phpmyadmin:
![[Mis apuntes/ANEXOS/Pasted image 20230312012341.png]]
Y ha funcionado:
![[Mis apuntes/ANEXOS/Pasted image 20230312012352.png]]
Pero también vimos que el puerto ssh está abierto, por lo que vamos a probar con esta contraseña y con el usuario notch, que es un usuario que podemos ver en la web:
![[Mis apuntes/ANEXOS/Pasted image 20230312012400.png]]
Por tanto en el ssh vamos a probar con este usuario y la contraseña que vimos antes; y ya estamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230312012409.png]]
Y ya tenemos la flag:
![[Mis apuntes/ANEXOS/Pasted image 20230312012416.png]]
Una vez dentro, podemos probar en escalar nuestros privilegios con el comando sudo su tratando de usar la misma contraseña que usamos para entrar por ssh, ya que vimos anteriormente que esta contraseña pertenecía a root, por lo que es fácil pensar que nos vuelva a funcionar:
![[Mis apuntes/ANEXOS/Pasted image 20230312014824.png]]
Y efectivamente ha funcionado y ya tenemos acceso a la flag de root:
![[Mis apuntes/ANEXOS/Pasted image 20230312014903.png]]