Aircrack-ng es la herramienta más conocida y utilizada para la realización de auditorías inalámbricas. Si alguna vez has probado la seguridad de WEP o WPA.
Dentro de la suite Aircrack-ng que sirve para crackear las contraseñas inalámbricas con WEP o WPA, también tenemos otras herramientas como Aireplay-ng que nos sirve para generar tráfico en un punto de acceso y hacer ataques de desautenticación, Airodump-ng que nos sirve para capturar todos los paquetes que viajan por el aire de los diferentes routers o AP inalámbricos al alcance, y también tenemos Airbase-ng que nos servirá para configurar puntos de acceso falsos y hacer que las víctimas se conecten a ellos para lanzar ataques de ingeniería social.

Primero verificamos que tenemos instalada la herramienta
apt-get install aircrack-ng
![[Pasted image 20240219191437.png|1000]]

Configuramos la tarjeta de red en modo monitor
airmon-ng start wlan0
![[Pasted image 20240219191532.png]]

Verificamos que este configurado correctamente
iwconfig
![[Pasted image 20240219191612.png]]

Ejecutamos el siguiente comando para realizar la busqueda de las redes wifi
airodump-ng wlan0
![[Pasted image 20240219192852.png]]
![[Pasted image 20240219192747.png]]

Nosotros vamos a atacar a nuestra red, para ello escribiremos el siguiente comando
airodump-ng -c 1 --bssid [mac] -w hacking wlan0
Primero seleccionamos la herramienta, el 5 estamos especificando el canal de escucha de la wifi, -w estamos indicando el nombre del fichero para guardar los resultados y finalmente seleccionamos nuestra tarjeta de red
![[Pasted image 20240219194533.png]]
![[Pasted image 20240219200756.png]]
En la ultima imagen podemos ver los equipos que están conectados a la red wifi que estamos analizando


Ahora necesitaremos generar trafico para encontrar el handshake, para ello escribiremos el siguiente comando
aireplay-ng -0 9 -a [MAC wifi] -c [MAC equipo red] wlan0 
![[Pasted image 20240219201612.png]]


Como podemos ver ya nos ha encontrado el handshake
![[Pasted image 20240219201812.png]]

Ahora podemos ver todos los listados que nos ha generado la herramienta, nosotros necesitaremos el archivo con la extensión .cap que es donde se almacena la información de la captura y ya lo tendremos todo para realizar el ataque
![[Pasted image 20240219202105.png]]

Con el siguiente comando realizariamos el ataque de diccionario
![[Pasted image 20240219202629.png]]
![[Pasted image 20240219202723.png]]

Ahora solo faltaria esperar que nos encontrase la contraseña