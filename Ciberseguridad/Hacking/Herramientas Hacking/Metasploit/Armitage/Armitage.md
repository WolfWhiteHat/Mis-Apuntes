Armitage es una interfaz gráfica de usuario (GUI) para el framework Metasploit. Fue desarrollado para hacer que Metasploit sea más accesible y fácil de usar para usuarios que prefieren una interfaz visual en lugar de la línea de comandos. Armitage proporciona funciones como la visualización de hosts en una red, la selección de exploits y payloads, el lanzamiento de ataques y la gestión de sesiones de acceso remoto.

Además de simplificar el proceso de realizar pruebas de penetración y ataques, Armitage también ofrece características como la colaboración en equipo, lo que permite a varios usuarios trabajar juntos en un proyecto de seguridad utilizando Metasploit. Esto lo convierte en una herramienta útil para profesionales de seguridad y equipos de prueba de penetración.


Para empezar a utilizar armitage primero tendremos que iniciar una base de datos, para ello ejecutaremos el sigueinte comando
`service postgresql start && msfconsole`
![[Pasted image 20240415115238.png]]

Una vez dentro de metasploit ejecutaremos el siguiente comando armitage, como se puede ver abre una pestaña, por defecto el usuario ya esta en la pestaña, unicamente le daremos a conectar
`armitage`
![[Pasted image 20240415115415.png]]

Nos saldra la sigueinte pestaña, le daremos en yes
![[Pasted image 20240415115514.png]]

En la siguiente imagen podemos ver el menu central de armitage, a la izquierda tenemos un menu para seleccionar los modulos, a la derecha nos mostrara los hosts que vayamos añadiendo y escanenado y abajo tenemos un termianal igual que en metasploit para poder navegar igual a parte de tener la versión de GUI
![[Pasted image 20240415115610.png]]

Para agregar un host tendremos que selecionar el menu de Hosts de la barra
![[Pasted image 20240415115818.png|350]]

Añadimos la ip
![[Pasted image 20240415115845.png|350]]

Y una vez añadido nos aparecera en la pestaña de la derecha
![[Pasted image 20240415115947.png]]

Si pulsamos clik derecho podremos realizar un escaneo basico
![[Pasted image 20240415120036.png]]

Una vez realizado el escaner podriamos profundizar mas y utilizar los modulos para realizar escaneo de los servicios y del sistema

Otra opción que tenemos es para ver los servicios al igual que en la terminal de metasploit 
![[Pasted image 20240415120143.png]]

Si realizamos un escaneo del SO nos mostrara en la pantalla que sistema utiliza y segun la versión la imagen cambia
![[Pasted image 20240415120314.png]]
![[Pasted image 20240415120428.png]]

