Realizamos un escaneo de nmap
![[Pasted image 20240604112935.png|1500]]

Encontramos el puerto 80 abierto, al analizarla encontramos que es una web de wordpress, asi que vamos a analizarla mas a fondo
![[Pasted image 20240604113127.png]]

Comenzamos con ver la version con whatweb
![[Pasted image 20240604113221.png]]

Ahora realizamos un escaneo con wpscan
```Bash
wpscan --url 10.10.98.55 -e vp,u
```
![[Pasted image 20240604122245.png]]
![[Pasted image 20240604122333.png]]

Nos ha encontrado varios usuarios, verificamos que estos usuarios existen
![[Pasted image 20240604114203.png|500]]

Ahora realizaremos un ataque de fuerza bruta con wpscan
```Bash
wpscan --url http://10.10.98.55 -U hugo,philip,c0ldd -P /home/wolf/rockyou.txt
```
![[Pasted image 20240604123247.png]]
![[Pasted image 20240604124814.png]]

Nos ha encontrado la password del usuario c0ldd y ya podemos acceder al wordpress
![[Pasted image 20240604125346.png]]

Ahora generaremos una reverse shell para obtener una sesion desde nuestra maquina atacante, para generarla modificaremos el codigo php de la pagina 404 del tema twentyfifteen
https://github.com/pentestmonkey/php-reverse-shell
![[Pasted image 20240604130358.png]]

Ahora nos ponemos a la escucha con netcat
![[Pasted image 20240604130524.png]]

Una vez estamos a la escucha ejecutaremos la siguiente url en el navegador
```Bash
http://10.10.98.55/wp-content/themes/twentyfifteen/404.php
```
![[Pasted image 20240604130640.png]]

Y ya habremos obtenido la reverse shell
![[Pasted image 20240604130721.png]]

Generamos una shell interactiva y una vez obtenida accedemos al fichero `wp-config.php` para obtener las credenciales de c0ldd
```Bash
cat /var/www/html/wp-config.php
```
![[Pasted image 20240604131043.png]]

O podemos utiliar el siguiente comando para encontrarlo automaticamente
```Bash
cat /var/www/html/wp-config.php | grep "DB_PASSWORD"
```
![[Pasted image 20240604131939.png]]

Ahora accedemos al usuario c0ldd
![[Pasted image 20240604131126.png]]

Ahora buscamos la primera flag
![[Pasted image 20240604131655.png]]


Ahora buscaremos realizar una escalada de privilegios para obtener permisos sudo, primero revisamos que podemos ejecutar como sudo
![[Pasted image 20240604132124.png]]

Podemos ejecutar tres comandos con privilegios de root, usaremos las tres para obtener los privilegios

## Escalda de privilegios con FTP
![[Pasted image 20240604133114.png]]

## Escalada de privilegios con VIM
![[Pasted image 20240604133324.png]]

