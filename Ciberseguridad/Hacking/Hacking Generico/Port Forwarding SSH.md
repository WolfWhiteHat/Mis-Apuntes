## Crear tunel inverso con SSH
Primero creamos las llaves de SSH
```Bash
ssh-keygen -f id_rsa
```
![[Pasted image 20240603090123.png]]

Copiamos la id de la clave publica
```Bash
cat id_rsa.pub
```
![[Pasted image 20240603090212.png]]

Añadimos la clave publica al fichero de `authorized_keys`
![[Pasted image 20240603090538.png]]
![[Pasted image 20240603093712.png]]

A la clave privada le añadimos los permisos `600`
```Bash
chmod 600 id_rsa
```
![[Pasted image 20240603095740.png]]

Y ahora ya podremos conectarnos con el siguiente comando
```Bash
ssh -i id_rsa -L 9001:127.0.0.1:9001 apaar@10.10.93.142
```
![[Pasted image 20240603095818.png]]

Ahora si accedemos al navegador y escribimos la ruta del puerto que hemos conectado por el puente veremos lo que hay configurado
![[Pasted image 20240603095905.png]]

[[MAQUINA CHILL HACK (Fuzzing web, fuerza bruta con BurpSuit, Reverse Shell con ejecución de comandos en web, TTY interactiva y portforwarding con Chisel y SSH]]

------


Para practicar el port forwarding con ssh vamos a practicar sobre la máquina [[MAQUINA INTERNAL (wordpress wpscan, hydra http, portforwarding chisel y hacking jenkins en docker)]], donde tenemos las siguientes credenciales para acceder vía SSH:
```
aubreanna:bubb13guM!@#123
```
![[Mis apuntes/ANEXOS/Pasted image 20231001125448.png]]

Y vemos que esta máquina tiene un jenkins corriendo por su puerto 8080:
![[Mis apuntes/ANEXOS/Pasted image 20230819120025.png]]

Vemos que efectivamente existe esta IP:
![[Mis apuntes/ANEXOS/Pasted image 20230819125930.png]]

También podemos confirmar si un puerto interno tiene un servicio corriendo con el comando netstat -tuln:
```
netstat -tuln
```
![[Mis apuntes/ANEXOS/Pasted image 20231001130051.png]]

Por tanto, desde nuestra máquina atacante ponemos el siguiente comando para decir que en mi puerto 5000 de mi máquina atacante esté corriendo el puerto interno 8080 de la máquina víctima:
```bash
ssh -L 5000:localhost:8080 aubreanna@10.10.218.157
```
![[Mis apuntes/ANEXOS/Pasted image 20231001125819.png]]

Y si ahora accedemos a mi puerto 5000 de mi máquina local vemos que accedemos correctamente:
![[Mis apuntes/ANEXOS/Pasted image 20231001125841.png]]



