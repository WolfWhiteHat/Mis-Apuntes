
Primero ejecutamos metasploit y seguidamente buscamos los modulos disponibles para proftpd, vamos a probar con el exploit numero 4
![[Pasted image 20240222130046.png]]

Revisamos la configuración del siguiente exploit
![[Pasted image 20240222130138.png]]

Configuramos la ip de la maquina victima y la opción SITEPATH, la cual define una ruta hacia un direcctorio del servidor
![[Pasted image 20240222130312.png]]

Ahora necesitaremos configurar un PAYLOAD, para ello seleccionaremos el siguiente PAYLOAD y la maquina con la cual vamos a tomar el control del equipo objetivo
![[Pasted image 20240222130535.png]]

Ejecutamos el exploit y como podemos ver ya obtenemos el acceso de la maquina victima
![[Pasted image 20240222130642.png]]


