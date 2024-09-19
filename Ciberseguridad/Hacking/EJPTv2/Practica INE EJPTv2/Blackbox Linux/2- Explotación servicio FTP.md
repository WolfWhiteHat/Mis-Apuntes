
Primero realizamos un escaneo del servicio a explotar
```
nmap -sV -sC -p21 10.2.26.53
```
![[Pasted image 20240430094836.png]]

Vemos que esta habilitado el servicio anonimo, lo probamos y vemos que tenemos acceso pero con funciones limitadas
![[Pasted image 20240430095223.png]]

Ahora vemos que nos marca una vulnerabilidad muy conocida, la del servicio vsftpd 2.3.4, intentamos acceder pero no obtendremos acceso porque esta vulnerabilidad abre una puerta trasera al puerto 6200 y esta cerrado
![[Pasted image 20240430095439.png]]

Revisamos la vulnerabilidad
![[Pasted image 20240430095519.png]]

La descargamos
![[Pasted image 20240430095608.png]]

Revisamos el codigo y vemos que la vulnerabilidad nos indica que intenta obtener acceso telnet por el puerto 6200
![[Pasted image 20240430095655.png]]

Le damos permisos y lo ejecutamos, como se puede ver la conexión ha sido rechazada
![[Pasted image 20240430095929.png]]

Revisamos y vemos el puerto 25 abierto, desde este servicio podemos explotarlo para enumerar usuarios
![[Pasted image 20240430100128.png]]

Ejecutaremos el siguiente modulo de metasploit
`auxiliary/scanner/smtp/smtp_enum`
![[Pasted image 20240430100737.png]]

Lo ejecutamos y obtenemos los usuarios
![[Pasted image 20240430101000.png]]

Ahora realizaremos un ataque de fuerza bruta al usuario service
```
hydra -l service -P /usr/share/metasploit-framework/data/wordlists/unix_users.txt 10.2.17.5 ftp
```
![[Pasted image 20240430101042.png]]

Probamos a acceder con el usuario y vemos que hemos obtenido acceso
![[Pasted image 20240430101247.png]]

Como al acceder la carpeta es la de /home sabemos que es un usuario
![[Pasted image 20240430101340.png]]

Ahora ya tenemos acceso al sistema y podemos navegar por los directorios
![[Pasted image 20240430101726.png]]

A diferencia de obtener una reverse shell son algunas limitaciones, pero si que podremos obtener muchisima información, si quisieramos obtener una reverse shell podriamos hacerlo creando un ejecutable con msfvenom, subirlo desde el acceso obtenido al servidor web que hay habilitado de WebDAV y ejecutarlo teniendo nuestra maquina como oyente con netcat, vamos realizar todo el proceso

Aqui vemos el servicio WebDAV habilitado donde podremos subir el ejecutable
![[Pasted image 20240430101959.png]]
![[Pasted image 20240430102024.png]]

Desde nuestra maquina de Kali Linux tenemos un fichero con las reverse shell configuradas, copiaremos el archivo en nuestro directorio para posteriormente configurarlo con nuestra ip
`/usr/share/webshells/php`
![[Pasted image 20240430102314.png]]

Lo editamos añadiendo nuestra ip y el puerto que queramos configurar
vim shell.php
![[Pasted image 20240430102529.png]]

En una pestaña nueva configuramos un oyente con netcat
```
nc -nvlp 1234
```
![[Pasted image 20240430103222.png]]

Como podemos ver intentamos subir el archivo y nos da un error, esto es porque solo podemos subir archivos en el directorio dav
![[Pasted image 20240430103651.png]]

Subimos el archivo
![[Pasted image 20240430103906.png]]

Y ahora lo ejecutamos desde el navegador
![[Pasted image 20240430103931.png]]

Y ya hemos obtenido el acceso desde la terminal donde estabamos de oyente con netcat
![[Pasted image 20240430104105.png]]

Ahora ya podríamos cargar cualquier archivo en todos los directorios
![[Pasted image 20240430104223.png]]
