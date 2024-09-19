Estos permisos permiten que un archivo se ejecute con los mismos privilegios de seguridad del usuario que lo posee, en lugar de con los permisos del usuario que lo ejecuta.

Ejecutamos el comando find / -perm -4000 2>/dev/null para comprobar donde tenemos permisos SUID (Se tratan de permisos que permiten a un usuario ejecutar un archivo con los privilegios del propietario del archivo), por tanto ejecutamos este comando:
```bash
find / -perm -u=s -type f 2>/dev/null
```
![[Mis apuntes/ANEXOS/Pasted image 20230306213232.png]]

El secreto aquí es buscar binarios de nombre extraño o binarios que generalmente no tengan el setuid activado; y salta a la vista el binario viewuser, por lo que lo vamos a inspeccionar:
![[Mis apuntes/ANEXOS/Pasted image 20230306213415.png]]

Para este caso en particular, vamos a entrar dentro y nos encontramos con un error donde nos dice que no encuentra la carpeta /tmp/listusers, además de poder intuir que esta herramienta ejecuta el comando que se encuentre dentro del fichero testusers, por lo que podemos usarlo para ver la flag de root:
![[Mis apuntes/ANEXOS/Pasted image 20230306213525.png]]

---------------------------------------------------------

## OTRO EJEMPLO 

Si hacemos una búsqueda de los permisos SUID, vemos que Python se encuentra entre ellos:
![[Mis apuntes/ANEXOS/Pasted image 20230401015128.png]]

Y también vemos estos permisos para Python:
![[Mis apuntes/ANEXOS/Pasted image 20230401015233.png]]

Por tanto nos creamos un fichero de Python con un código que nos permita escalar privilegios:
![[Mis apuntes/ANEXOS/Pasted image 20230401015723.png]]

Lo compartimos con la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230401015746.png]]

Y lo ejecutamos para convertirnos en root:
![[Mis apuntes/ANEXOS/Pasted image 20230401015812.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401015823.png]]
[[MAQUINA ROOTME (Fuzzing, php malicioso camuflándolo como phtml en burpsuite, escalada de privilegios comprobando permisos SUID de Python)]]


------
Una herramienta para automatizar el proceso de busqueda de ficheros con permisos SUID es 
[suid3num.py](https://github.com/Anon-Exploiter/SUID3NUM)

Para ello primero nos descargamos la herramienta en nuestra maquina
```Bash
wget https://raw.githubusercontent.com/Anon-Exploiter/SUID3NUM/master/suid3num.py --no-check-certificate && chmod 777 suid3num.py
```
![[Pasted image 20240613113209.png]]

Lo cargamos en la maquina victima
![[Pasted image 20240613113314.png]]

Y ahora lo ejecutamos, como podemos ver nos automatiza el encontrarnos los binarios e indicarnos que comando ejecutar
![[Pasted image 20240613113410.png]]
![[Pasted image 20240613113428.png]]
[[MAQUINA AIRPLANE (Fuzzing web, explotación LFI con script en python,  acceso cargando paylaod por GDB Server, escalada de privilegios con vulnerabilidad SUID y escalada a root revisando permisos sudo)]]