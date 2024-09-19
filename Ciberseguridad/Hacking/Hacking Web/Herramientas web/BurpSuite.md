Burp suite es un escáner de vulnerabilidades web y una de las herramientas más conocidas y utilizadas para realizar auditorías de seguridad de aplicaciones web, es un proxy de interceptación, es un intermediario entre el navegador y el servidor web

Primero antes de empezar a utilizarlo tendremos que instalarlo en nuestro sistema
![[Pasted image 20240205103556.png]]

Una vez dentro de BupSuite iremos a la configuración del proxy
![[Pasted image 20240205121850.png]]
Como podemos ver ya estamos dentro, ahora configuraremos el proxy en el navegador para que el programa pueda hacer de intermediario e interceptar el trafico

Como podemos ver en la siguiente imagen ya tenemos configurado el proxy en nuestro navegador
![[Pasted image 20240205122029.png]]

Ahora le daremos a intercept is of y activaremos la herramienta para que escuche todo el trafico
![[Pasted image 20240205122133.png]]

Una vez este activado y estemos en la pestaña donde queremos interceptar el trafico, solo tenemos que ejecutar la acción de login
![[Pasted image 20240205122857.png]]

Al ejecutarlo se nos abrira la herramienta con el trafico capturado
![[Pasted image 20240205122940.png]]

Una vez tenemos el trafico capturado, si le damos a Ctrl+r nos aparecera la siguiente pestaña la cual nos permite interactuar con la web directamente y obtener la respuesta, esto es muy útil cuando por ejemplo queremos acceder a una web con las credenciales pero nos obligan a poner un correo, podemos poner uno de ejemplo, capturar el trafico y dentro de BurnSuite modificar el contenido que queramos, por ejemplo hacer un ataque de SQL Injectio ' or 1=1-- -'
![[Pasted image 20240205123143.png]]

Una vez hemos terminado de utilizar la herramienta volveremos a dejar la configuración del navegador como la teniamos antes, quitando la configuración proxy
