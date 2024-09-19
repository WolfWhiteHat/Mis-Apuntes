**ssh-keygen** es un componente estándar de los paquetes de protocolos **Secure Shell (SSH)** que se encuentran en los sistemas informáticos **Unix** y Microsoft **Windows**. Estos protocolos se utilizan para establecer sesiones de shell seguras entre computadoras remotas a través de redes inseguras, mediante el uso de diversas técnicas criptográficas.

![[Pasted image 20240604083912.png]]

Crearemos una clave de ssh y la subiremos
```Bash
ssh-keygen -f id_rsa
```
![[Pasted image 20240604082513.png]]

Renombramos la clave publica para subir el archivo a la maquina victima
![[Pasted image 20240604082730.png]]

Subimos la clave publica
![[Pasted image 20240604083027.png]]

Revisamos que se haya subido nuestra clave publica
![[Pasted image 20240604083053.png]]

Y ahora ya podriamos acceder por ssh y obtener acceso a la maquina victima
![[Pasted image 20240604083253.png]]


# Realizar portforwarding con SSH
Dentro de este documento de txt nos indica que este servicio corre por el puerto 8111 por defecto, lo revisamos con ss ya que no disponemos de netcat
```Bash
ss -tn
```
![[Pasted image 20240604085431.png]]

Antes de ejecutar el comando para realizar portforwarding con ssh, cambiaremos los permisos a nuestra clave privada
```Bash
chmod 600 id_rsa
```
![[Pasted image 20240604090115.png]]

Lo encontramos abierto, ahora para poder acceder necesitamos hacer portforwarding, para ello ejecutaremos el siguiente comando con ssh desde nuestra maquina atacante
```Bash
ssh -i id_rsa -L 8111:127.0.0.1:8111 sys-internal@10.10.19.73
```
![[Pasted image 20240604085834.png]]

Si ahora vamos al navegador veremos el servicio por el puerto que esta corriendo la maquina
![[Pasted image 20240604085955.png]]

[[MAQUINA VULNET INTERNAL (Subida de fichero con redis, obtencion de acceso y portforwarding con SSH, escalada de privilegios fichero sudoers.d]]