En esta máquina se está corriendo un servicio de MySQL dentro del puerto 3306:
![[Mis apuntes/ANEXOS/Pasted image 20230509115021.png]]
INICIAR SESIÓN BASE DE DATOS SIN CREDENCIALES:
Para iniciar sesión en una base de datos usamos la opción -u y podemos usar el usuario root para iniciar sesión sin la contraseña, para ello voy a usar docker para ejecutar mysql y desde ahí lanzo el comando mysql -h 10.129.95.232 -u root para entrar dentro de la base de datos del host de destino:
![[Mis apuntes/ANEXOS/Pasted image 20230509115037.png]]
Para ver las bases de datos:
![[Mis apuntes/ANEXOS/Pasted image 20230509115047.png]]
Elegimos la base de datos que queramos extraer la información:
![[Mis apuntes/ANEXOS/Pasted image 20230509115055.png]]
Para ver las tablas:
![[Mis apuntes/ANEXOS/Pasted image 20230509115103.png]]
Y dentro de config tenemos la flag:
![[Mis apuntes/ANEXOS/Pasted image 20230509115112.png]]
