Vamos a empezar la prueba de caja negra identificando la ip, para ello la buscaremos en la carpeta `/etc/hosts`
![[Pasted image 20240423084333.png]]
![[Pasted image 20240423084358.png]]


Hacemos un ping y por el TTL vemos que esta corriendo un SO Windows
![[Pasted image 20240423084428.png]]


Realizaremos un escaneo de la maquina victima y prepararemos el escaneo para importarlo a metasploit
```
nmap -T4 -PA -sC -sV -p 1-10000 10.2.22.236 -oX nmap_10k
```
![[Pasted image 20240423084552.png]]
![[Pasted image 20240423084634.png]]
![[Pasted image 20240423084659.png]]
![[Pasted image 20240423084721.png]]
![[Pasted image 20240423084755.png]]


Intentamos ver la versión del servicio ftp sin resultado
```
nc -nv 10.2.22.236 21
```
![[Pasted image 20240423084151.png]]


Detectamos varios servicio http activos, vamos a revisarlos
`Puerto 80`
![[Pasted image 20240423082032.png]]

`Puerto 4848`
![[Pasted image 20240423082127.png]]

`Puerto 5985`
![[Pasted image 20240423082223.png]]

`Puerto 8080`
![[Pasted image 20240423082257.png]]

`Puerto 8484`
![[Pasted image 20240423082337.png]]

`Puerto 8585`
![[Pasted image 20240423082412.png]]

`Puerto 47001`
![[Pasted image 20240423082455.png]]

Iniciamos la consola de metasploit y el servidor de postgresql para subir el escaneo de nmap a metasploit
![[Pasted image 20240423081754.png]]

Importamos el escaneo
![[Pasted image 20240423085254.png]]

Como podemos ver ya se ha importado el escaneo
![[Pasted image 20240423085323.png]]

Como no vemos el nombre buscaremos la versión de smb
![[Pasted image 20240423085706.png]]

Y como podemos ver ya nos ha enumerado el nombre de la maquina
![[Pasted image 20240423085741.png]]

Aquí tenemos algo por donde podriamos empezar a buscar vulnerabilidades
![[Pasted image 20240423085824.png]]