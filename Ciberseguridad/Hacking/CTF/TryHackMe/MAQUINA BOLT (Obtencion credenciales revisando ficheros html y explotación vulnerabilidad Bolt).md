Realizamos un escaneo de nmap
![[Pasted image 20240603124654.png]]

Encontramos abiertos el puerto 22, 80 y 8000.

Revisamos y encontramos que el puerto 8000 hay configurado un servicio http, analizando la web encontramos de primeras un posible usuario
![[Pasted image 20240603124829.png]]

Analizando el codigo de la web encontramos un mensaje con una posible password
![[Pasted image 20240603124923.png]]

Encontramos otro posible nombre de usuario
![[Pasted image 20240603125118.png]]

Accedemos al portal de login del cms de bolt
![[Pasted image 20240603133152.png]]

Y con las credenciales obtenidas en la web obtenemos acceso al portal
User: `bolt`
passwd: `boltadmin123`
![[Pasted image 20240603133251.png]]

Ahora tenemos dos opciones para insertar un payload, de forma manual y automatica, comenzaremos de forma automatica injectando un payload desde un modulo de metasploit
`explit/unix/webapp/bolt_authenticated_rce`, lo cargamos y configuramos
![[Pasted image 20240603140630.png]]

Y al ejecutarlo obtenemos la reverse shell
![[Pasted image 20240603140654.png]]
![[Pasted image 20240603140815.png]]

