
Primero tendremos que saber donde se ubican los hashesh en Linux, el cual la ruta donde se estan ubicados es `/etc/shadow`, solo podremos acceder a estos documentos con privilegios de root, posteriormente crackearemos los hashesh con John the Ripper

A diferencia de Windows que es automatico desde Meterpreter con el comando de hashdump, en Linux tendremos que cargar un modulo manualmente y configurarlo, para ello primero tendremos que obtener acceso en la maquina victima

Primero necesitaremos obtener acceso a la maquina con privilegios de root
![[Pasted image 20240411082551.png]]


Una vez obtenidos los privilegios de root actualizaremos la sesion a meterpreter para posteriormente cargar el modulo
![[Pasted image 20240411082757.png]]

Ahora seleccionaremos el siguiente modulo
`post/linux/gather/hasdump`
![[Pasted image 20240411082831.png]]

Una vez seleccionado lo configuramos y cargamos, en la siguiente imagen podemos ver que se ha ejecutado correctamente pero no ha mostrado nada porque el ordenador al que hemos atacado no tiene contraseñas configuradas
![[Pasted image 20240411082953.png]]

Si escribimos loot podremos ver los archivos que ha recogido, leeremos el archivo de `/etc/shadow`, como podemos ver aparece un asterisco porque no tiene contraseñas por defecto, esto es normal para los usuarios que se crear para los servicios
![[Pasted image 20240411084851.png]]

Vamos a configurarle una contraseña al usuario root y crear otro usuario de prueba
![[Pasted image 20240411084659.png]]


Volvemos a cargar el modulo y como podemos ver ahora si nos ha cargado los hasehs
![[Pasted image 20240411085147.png]]

Ahora revisamos los archivos y los volvemos a leer y en este caso si que ya aparecen los hasesh
![[Pasted image 20240411085235.png]]

