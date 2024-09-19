Los script que estan creados por defecto se encuentran en la siguiente ruta
`/usr/share/metasploit-framework/scripts/resource/`

Para crear un scrip utilziaremos un editor y crearemos el scrip con el contenido que queramos ejecutar, como veremos en la siguiente imagen en un editor de texto hemos añadido los comandos que ejecutariamos en la consola de metasploit
![[Pasted image 20240325192319.png]]

Una vez creado el scrip para ejecutarlo utilziaremos el siguiente comando
`msfconsole -r handler.rc

Con el siguiente comando cargaremos el script en metasploit
`resource ~/Desktop/handler.rc`