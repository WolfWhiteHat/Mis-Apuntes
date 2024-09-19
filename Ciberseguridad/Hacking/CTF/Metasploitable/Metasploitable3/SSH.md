c
Como podemos ver en el escaner esta abierto el puerto 22, ahora vamos a explotarlo.

Lo primero sera abrir metasploit y ejecutar un auxiliar para comprobar todos los usuarios que hay en el servidor, la idea sera ejecutar un ataque de fuerza bruta para acceder al equipo y tomar el control.

Para ello seleccionaremos el auxiliary enumusers y dentro configuraremos 
![[Pasted image 20240222132509.png|1000]]

Como podemos ver en la siguiente imagen, nos ha dado un falso positivo y el escaneo a sido abortado, si creemos que puede ser un falso positivo podemos marcar la opción 'CHECK_FALSE' en 'false' y en caso de que vuelva a detectarlo nos seguira realizando el escaneo
![[Pasted image 20240226082244.png]]

Como podemos ver en la siguiente imagen ya nos ha encontrado los usuarios creados en el sistema
![[Pasted image 20240226082411.png|500]]




https://sysadblog.onrender.com/posts/metasploitable3/

