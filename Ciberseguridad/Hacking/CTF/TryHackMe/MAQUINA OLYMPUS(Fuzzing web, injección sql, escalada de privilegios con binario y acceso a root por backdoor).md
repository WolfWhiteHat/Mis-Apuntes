Realizamos un escaneo con nmap
![[Pasted image 20240611130812.png]]

Detectamos dos puertos abiertos, el 22 y el 80, empezaremos analizando el puerto 80, para ello comenzaremos haciendo fuzzing web
```Bash
dirsearch -u http://olympus.thm -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -e php,html, js
```
![[Pasted image 20240611130547.png]]

Analizamos el ultimo enlace y encontramos que es un CMS muy vulnerable
![[Pasted image 20240611130927.png]]

Revisando encontramos la siguiente vulnerabilidad del CMS
![[Pasted image 20240611131635.png]]

Revisamos y comenzaremos explotando esta vulnerabilidad
```
https://www.exploit-db.com/exploits/48734
```

Esta vulnerabilidad indica que podemos hacer una injección de SQL mediante la explotación del campo search de la siguiente url
```
http://olympus.thm/~webmaster/search.php
```

Ejecutamos el siguiente comando con la herramienta sqlmap y encontramos que es vulnerable a la injección de sql
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" --dbs --random-agent -v 3
```
![[Pasted image 20240611135709.png]]

Ahora ejecutamos el sigueinte comando para enumerar la base de datos
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" -D olympus --tables --random-agent -v 3
```
![[Pasted image 20240611140217.png]]

Ejecutando el siguiente comando obtenemos la primera flag y los siguientes usuarios
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" -D olympus --dump-all --random-agent -v 3
```
![[Pasted image 20240611141126.png]]
Usuario: prometheus
Email: prometheus@olympus.thm
Rol: User
Hash de contraseña: $2y$10$YC6uoMwK9VpB5QL513vfLu1RV2sgBf01c0lzPHcz1qK2EArDvnj3C

Usuario: root
Email: root@chat.olympus.thm
Rol: Admin
Hash de contraseña: $2y$10$lcs4XWc5yjVNsMb4CUBGJevEkIuWdZN3rsuKWHCc.FGtapBAfW.mK

Usuario: zeus
Email: zeus@chat.olympus.thm
Rol: User
Hash de contraseña: $2y$10$cpJKDXh2wlAI5KlCsUaLCOnf0g5fiG0QSUS53zp/r0HMtaj6rT4lC

Ahora utilizaremos john the ripper para descifrar las contraseñas de estos usuarios
```Bash
john --format=bcrypt --wordlist=~/rockyou.txt users.txt
```
![[Pasted image 20240611143230.png]]
![[Pasted image 20240611143253.png]]

Ahora probaremos a acceder con las credenciales obtenidas
![[Pasted image 20240611143656.png]]

Y ya estamos dentro del panel del cms
![[Pasted image 20240611143719.png]]


Revisando la información encontramos que varios usuarios estan logueados con el dominio de `chat.olympus.thm` lo agregamos a nuestro host y probamos a acceder
![[Pasted image 20240612075626.png]]

Al buscarlo en el navegador podemos ver que encontramos acceso a otro panel
![[Pasted image 20240612075740.png]]

Probamos a loguearnos con las credenciales previamente obtenidas y obtenemos resultado
![[Pasted image 20240612075835.png]]

Vamos a proceder a realizar una enumeración de este dominio
![[Pasted image 20240612080539.png]]

Encontramos una ruta de uploads la cual aparentemente podemos ver los archivos que subimos, en el chat revisamos y encontramos una coincidencia de un archivo subido con la información obtenida con la inyección de sql en la cual encontramos el archivo con el nombre cambiado
![[Pasted image 20240612080817.png]]

Cogemos el nombre del archivo subido y encontramos que podemos acceder
![[Pasted image 20240612081052.png]]

Ahora intentaremos subir una carga maliciosa para obtener una reverse shell, cargamos la shell
![[Pasted image 20240612081500.png]]

La buscamos para ver como lo ha guardado en la base de datos volviendo a ejecutar la injeccion de sql con sqlmap agregando el parametro fresh-queries para refrescar los resultados y como podemos ver se ha subido lo que hemos cargado
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" -D olympus --dump-all --random-agent -v 3 --fresh-queries

```
![[Pasted image 20240612081758.png]]

Nos ponemos en escucha con netcat, ejecutamos el archivo y obtenemos la reverse shell
![[Pasted image 20240612081916.png]]
![[Pasted image 20240612081931.png]]

Ahora crearemos una shell estable y empezaremos a intentar obtener una escalada de privilegios, revisando encontramos la segunda flag y el siguiente mensaje
![[Pasted image 20240612082612.png]]

Buscaremos realizar una escalada al usuario zeus para posteriormente obtener acceso como root, revisando los binarios encontramos uno que es sospechoso
```Bash
find / -perm -4000 2>/dev/null
```
![[Pasted image 20240612084039.png]]

Ejecutamos el binario y descubrimos que se utiliza para extraer ficheros
![[Pasted image 20240612090029.png]]

Si intentamos extraer el la clave privada encontrariamos que no tenemos permisos
![[Pasted image 20240612090126.png]]

Así que nos copiamos la clave privada e intentamos acceder al sistema por ssh
![[Pasted image 20240612090314.png]]

No obtenemos acceso porque nos solicita la password, asi que extraeremos el id a hash para luego intentar crackearlo
![[Pasted image 20240612090542.png]]

Ahora con john the ripper crackearemos el hash
```Bash
john --format=SSH zeus.hash
```
![[Pasted image 20240612093005.png]]

Ahora cambiamos los permisos del archivo con la clave privada para poder acceder al sistema
![[Pasted image 20240612094028.png]]

Revisando la carpeta de zeus encontramos la siguiente información
![[Pasted image 20240612094741.png]]

Parece ser un archivo de configuración para gestionar contenedores en Linux, intentamos revisar los contenedores pero no tenemos permisos
```Bash
lxc image list images
```
![[Pasted image 20240612095749.png]]

Continuamos buscando información y encontramos una carpeta sospechosa la cual al acceder encontramos un archivo php que al leerlo nos proporciona una configuración de una reverse shell
![[Pasted image 20240612104402.png]]

Ahora accedemos a la url del archivo y nos aparece para escribir una password
![[Pasted image 20240612111727.png]]

Al escribirla nos indica los parametros para poder obtener la reverse shell
![[Pasted image 20240612111812.png]]


Ahora escribimos arriba en el navegador el comando que aparece abajo y ya habremos obtenido la reverse shell como root
![[Pasted image 20240612145253.png]]
![[Pasted image 20240612145309.png]]

Y ya podremos obtener la flag
![[Pasted image 20240612145438.png]]

Escribiendo el siguiente comando obtenemos la ubicación de la flag oculta
```Bash
grep -irl flag{ /etc/
```
![[Pasted image 20240612150521.png]]