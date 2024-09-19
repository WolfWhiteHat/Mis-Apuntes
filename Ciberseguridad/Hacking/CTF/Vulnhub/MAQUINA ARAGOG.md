Empezamos con la primera máquina, la cual es la máquina aragog, por lo que hacemos el reconocimiento con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230813124746.png]]
Esto es lo que corre por el puerto 80:
![[Mis apuntes/ANEXOS/Pasted image 20230813124953.png]]
Hacemos fuzzing con gobuster y nos encontramos con el directorio /blog:
![[Mis apuntes/ANEXOS/Pasted image 20230813125158.png]]
Por lo que si lo ponemos en el navegador vemos que no carga bien, posiblemente porque se esté aplicando virtual hosting:
![[Mis apuntes/ANEXOS/Pasted image 20230813125222.png]]
No obstante, si miramos el código fuente, vemos que tenemos una dirección la cual es la siguiente:
```bash
http://wordpress.aragog.hogwarts
```
![[Mis apuntes/ANEXOS/Pasted image 20230813125251.png]]
Por lo que lo añadimos al /etc/hosts:
![[Mis apuntes/ANEXOS/Pasted image 20230813125406.png]]
Y ahora ya nos carga bien la página:
![[Mis apuntes/ANEXOS/Pasted image 20230813125428.png]]
Por tanto, al ver que estamos ante un wordpress, vamos a enumerar usuarios y plugins vulnerables con wpscan, utilizando los siguientes parámetros:
```bash
wpscan --url http://192.168.0.16/blog/ --enumerate u,vp
```
Y nos encuentra el usuario admin y la versión de wordpress 5:
![[Mis apuntes/ANEXOS/Pasted image 20230813125711.png]]
De todos modos, si queremos enumerar de forma más eficiente, tenemos que usar la API de wpscan:
![[Mis apuntes/ANEXOS/Pasted image 20230813130302.png]]
Y si investigamos sobre ese file manager unauthenticated, vemos que tenemos una prueba de concepto dentro de la web oficial de wpscan:
![[Mis apuntes/ANEXOS/Pasted image 20230813130424.png]]
Podemos descargarnos este script de python:
![[Mis apuntes/ANEXOS/Pasted image 20230813130513.png]]
Pero dentro de este script, vemos que en las instrucciones se menciona que lee el contenido de un archivo payload.php:
![[Mis apuntes/ANEXOS/Pasted image 20230813130627.png]]
Por lo que tenemos que crearlo y ahí meter el código malicioso de php:
![[Mis apuntes/ANEXOS/Pasted image 20230813130728.png]]
Y ahora si lanzamos el script, se habrá subido este código malicioso en la ruta que nos indican:
![[Mis apuntes/ANEXOS/Pasted image 20230813130846.png]]
Pero vemos que la url no está del todo bien representada, por lo que simplemente la pegamos en el navegador de forma corregida y ya estará arreglado:
```bash
http://192.168.0.16/blog//wp-content/plugins/wp-file-manager/lib/files/payload.php?cmd=whoami
```
Y podremos ejecutar comandos de forma remota:
![[Mis apuntes/ANEXOS/Pasted image 20230813131002.png]]
Ahora para ganar acceso a la máquina víctima, url encodeamos el código malicioso para enviarnos una reverse shell y habremos recibido la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230813131517.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230813131524.png]]
Y recibimos la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230813131540.png]]
Dentro del directorio home visualizamos los 2 usuarios:
![[Mis apuntes/ANEXOS/Pasted image 20230813131838.png]]
Una vez dentro, visualizamos un fichero de la configuración de wordpress donde se guarda una contraseña, la cual es mySecr3tPass:
![[Mis apuntes/ANEXOS/Pasted image 20230813132130.png]]
Por tanto intentamos usarla para conectarnos a la base de datos y vemos que funciona:
![[Mis apuntes/ANEXOS/Pasted image 20230813132206.png]]
Dentro de la base de datos wordpress encontramos estas tablas:
![[Mis apuntes/ANEXOS/Pasted image 20230813132307.png]]
Y tenemos la contraseña de hadrid:
![[Mis apuntes/ANEXOS/Pasted image 20230813132357.png]]
Guardamos este hash para intentar crackearlo:
![[Mis apuntes/ANEXOS/Pasted image 20230813132450.png]]
Y vemos que la contraseña es password123:
![[Mis apuntes/ANEXOS/Pasted image 20230813132536.png]]
```bash
hagrid98:password123
```
Y podemos entrar por ssh:
![[Mis apuntes/ANEXOS/Pasted image 20230813132721.png]]
Podemos buscar scripts de bash dentro del sistema con este comando de find:
```bash
find / -name *.sh 2>/dev/null
```
Y nos encontramos con un backup.sh:
![[Mis apuntes/ANEXOS/Pasted image 20230813133026.png]]
Y vemos este contenido:
![[Mis apuntes/ANEXOS/Pasted image 20230813133047.png]]
Y alteramos el contenido del script para cambiar permisos a la bash:
![[Mis apuntes/ANEXOS/Pasted image 20230813133138.png]]
Y ya somos root:
![[Mis apuntes/ANEXOS/Pasted image 20230813133242.png]]
