Haremos los reconocimientos de siempre:
![[Mis apuntes/ANEXOS/Pasted image 20230520160029.png]]
Vemos que tenemos el FTP anonymous login allowed:
![[Mis apuntes/ANEXOS/Pasted image 20230520160356.png]]
Y vamos a descargarnos todos los archivos que están dentro del ftp:
![[Mis apuntes/ANEXOS/Pasted image 20230520160421.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230520160435.png]]
Podemos ver que el script.sh hace una especie de limpieza y parece que lo hace de forma automatizada:
![[Mis apuntes/ANEXOS/Pasted image 20230520160549.png]]
Por tanto vamos a sustituir este fichero por uno que incluya una reverse shell y subirlo a la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230520160642.png]]
Y lo subimos con el comando put (previamente tenemos que autenticarnos):
![[Mis apuntes/ANEXOS/Pasted image 20230520160830.png]]
Y ahora que hemos subido este código con la reverse shell, tenemos que ponernos en escucha con netcat y habremos recibido la reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230520160945.png]]
Una vez dentro, tras hacer varias investigaciones, vemos que si buscamos binarios SUID vemos el de env, el cual es vulnerable:
![[Mis apuntes/ANEXOS/Pasted image 20230522161522.png]]
Y ahora podemos lanzarnos una bash como root usando este binario de la siguiente forma:
![[Mis apuntes/ANEXOS/Pasted image 20230522161633.png]]
