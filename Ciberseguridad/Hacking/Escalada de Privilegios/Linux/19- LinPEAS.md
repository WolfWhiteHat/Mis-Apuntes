Se trata de una herramienta similar a [[1 - Linux Exploit Suggester]], que nos sirve para hacer un reconocimiento de la máquina víctima para encontrar formas de escalar los privilegios. Por tanto este es el repositorio:
```
https://github.com/peass-ng/PEASS-ng
```
![[Pasted image 20240607095143.png]]

Ahora realizaremos una escalada de privilegios para ello utilizaremos una herramienta para la busqueda de vulnerabilidades llamada LinPEAS, para ello primero la descargamos en nuestra maquina
```
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
```
![[Pasted image 20240607100351.png]]

Cargamos un servidor de python para subir el binario
![[Pasted image 20240607100434.png]]

Y nos lo descargamos en la maquina victima
![[Pasted image 20240607100803.png]]

Agregamos los permisos de ejecución
![[Pasted image 20240607100948.png]]

Y ejecutamos el binario en la maquina victima y ya comenzara a buscar las posibles vulnerabilidades
![[Pasted image 20240607101037.png]]

