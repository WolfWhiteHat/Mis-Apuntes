Realizamos un escaneo de nmap y encontramos los siguientes puertos abiertos
![[Pasted image 20240626075957.png|500]]

Ahora continuaremos analizandolos, revisamos el puerto 80 y encontramos el siguiente portal
![[Pasted image 20240626080043.png|500]]

Hacemos fuzzing web y encontramos los siguientes directorios
![[Pasted image 20240626082253.png]]

Accedemos por el servicio ftp de forma anonima y encontramos una imagen
![[Pasted image 20240626080320.png]]

Nos descargamos la imagen
![[Pasted image 20240626080408.png]]

Revisamos con steghide y encontramos que contiene información
![[Pasted image 20240626080532.png]]

Leemos el fichero y encontramos el contenido cifrado en base64
![[Pasted image 20240626080600.png]]

Lo decodificamos
![[Pasted image 20240626081336.png]]

Y encontramos los usuarios del sistema
![[Pasted image 20240626081413.png]]

Verificamos que tipo de hash es
![[Pasted image 20240626081754.png]]

Ahora decodificaremos la password del usuario Charlie
![[Pasted image 20240626111251.png]]

Al probar las credenciales en el panel del login obtenemos acceso
![[Pasted image 20240626111347.png]]

Tenemos un panel para poder ejecutar comandos, asi que nos generamos una reverse shell y obtenemos acceso desde el terminal
![[Pasted image 20240626111750.png]]

Ejecutamos pspy64 en la maquina victima y obtenemos un proceso los cuales podrian ser vulnerables
![[Pasted image 20240626112414.png]]

Abrimos el archivo ports.sh y obtenemos el siguiente script
![[Pasted image 20240626112910.png]]

El script hace lo siguiente
- **Escucha en múltiples puertos**: Utiliza `netcat` (`nc`) para escuchar en varios puertos (100-112 y 114-125).
- **Redireccionamiento de salida**: Los datos recibidos en los puertos especificados se redirigen al archivo `/etc/init.d/chocolate.txt`.
- **Anuncio en el puerto 113**: Se publica un mensaje en el puerto 113 utilizando `netcat`.

Probamos y vemos que la maquina esta en escucha
![[Pasted image 20240626114925.png]]

Si probamos a conectarnos a los otros puertos nos lista el siguiente mensaje
![[Pasted image 20240626115203.png]]

Revisamos y encontramos que en el directorio de charlie tenemos la clave privada
![[Pasted image 20240626115347.png]]

Probamos a acceder con la clave privada y ya tenemos acceso como Charlie
![[Pasted image 20240626120127.png]]
![[Pasted image 20240626120148.png]]

Revisamos los permisos sudo de charlie y encontramos que puede ejecutar vi
![[Pasted image 20240626120241.png]]

Buscamos la vulnerabilidad en GTFOBins
![[Pasted image 20240626120321.png]]

Y al probarlo obtenemos permisos de root
![[Pasted image 20240626120346.png]]

Al buscar la flag de root encontramos que nos pide una key
![[Pasted image 20240626120524.png]]

Buscamos la clave que se encuentra en el directorio de `/var/www/html/
![[Pasted image 20240626120857.png]]
![[Pasted image 20240626120824.png]]

Ahora escribimos la contraseña y ya obtenemos la flag de root
![[Pasted image 20240626121110.png]]


