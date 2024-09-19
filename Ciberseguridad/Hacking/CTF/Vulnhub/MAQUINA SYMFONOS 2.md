Hacemos el escaneo de puertos con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230914154812.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230914154827.png]]
Nos encontramos con el puerto 445 abierto, por lo que vamos a inspeccionar este puerto:
```bash
smbmap -H 192.168.0.59
```
Y nos encontramos con el recurso compartido anonymous/backups y dentro un log.txt:
![[Mis apuntes/ANEXOS/Pasted image 20230914154914.png]]
Por lo que lo descargamos:
```bash
smbmap -H 192.168.0.59 --download anonymous/backups/log.txt
```
Y aquí vemos que existe un usuario llamado aeolus y que además hay una copia del fichero /etc/shadow:
![[Mis apuntes/ANEXOS/Pasted image 20230914155057.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230914155123.png]]
Y por samba vemos que podemos acceder al repositorio de _/home/aeolus/share_, pero no hay más información, por lo que vamos a investigar el puerto 21, donde vemos que tenemos una versión de proFTPD 1.3.5; y en searchsploit vemos que es vulnerable y podemos copiar archivos internos de la máquina:
![[Mis apuntes/ANEXOS/Pasted image 20230917113437.png]]
Por tanto procedemos a copiar esa copia del fichero shadow:
![[Mis apuntes/ANEXOS/Pasted image 20230917113409.png]]
Y ahora ya podemos localizar el fichero shadow que acabamos de mover:
```bash
smbmap -H 192.168.0.64 -r anonymous
```
![[Mis apuntes/ANEXOS/Pasted image 20230917113559.png]]
Lo descargamos:
```bash
smbmap -H 192.168.0.64 --download anonymous/shadow.bak
```
![[Mis apuntes/ANEXOS/Pasted image 20230917113639.png]]
No obstante, este fichero shadow viene protegido, por lo que tendremos de crackearlo con john the ripper:
![[Mis apuntes/ANEXOS/Pasted image 20230917113656.png]]
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt shadow
john --show shadow
```
![[Mis apuntes/ANEXOS/Pasted image 20230917113836.png]]
Y tenemos estas credenciales:
```bash
aeolus:sergioteamo
```
Vemos que funcionan:
![[Mis apuntes/ANEXOS/Pasted image 20230917113901.png]]
Dentro de /opt tenemos un directorio algo extraño:
![[Mis apuntes/ANEXOS/Pasted image 20230917114241.png]]
Ejecutamos el comando ps -aux para ver qué procesos están corriendo en mi sistema, y vemos algo de apache:
![[Mis apuntes/ANEXOS/Pasted image 20230917114358.png]]
Y con el comando ss -tuln vemos que por el puerto 8080 está corriendo algo, seguramente el servidor de apache:
![[Mis apuntes/ANEXOS/Pasted image 20230917114454.png]]
El siguiente paso será realizar port forwarding con ssh, por lo que en nuestra máquina atacante comprobamos que esté activo el servicio de ssh:
![[Mis apuntes/ANEXOS/Pasted image 20230917114552.png]]
Ahora ejecutamos el siguiente comando desde nuestra máquina atacante para traernos el puerto 8080 de la máquina víctima a la atacante:
```bash
ssh -L 5000:localhost:8080 aeolus@192.168.0.64
```
![[Mis apuntes/ANEXOS/Pasted image 20230917114852.png]]
Y dentro del puerto 5000 nos encontramos con lo siguiente:
![[Mis apuntes/ANEXOS/Pasted image 20230917114943.png]]
Probamos en entrar con las credenciales que ya tenemos:
```bash
aeolus:sergioteamo
```
Hacemos una búsqueda en busca de vulnerabilidades de este servicio y nos encontramos con el siguiente exploit:
![[Mis apuntes/ANEXOS/Pasted image 20230917115134.png]]
Por tanto ponemos este CVE en metasploit y vemos que estamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230917115729.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230917115738.png]]
Cambiamos a la bash y vemos que con sudo -l podemos ejecutar mysql:
![[Mis apuntes/ANEXOS/Pasted image 20230917115811.png]]
Vemos las instrucciones en gtfobins de como escalar privilegios explotando esto:
![[Mis apuntes/ANEXOS/Pasted image 20230917115857.png]]
Y lo aplicamos y vemos que ya somos el usuario root:
![[Mis apuntes/ANEXOS/Pasted image 20230917115918.png]]
