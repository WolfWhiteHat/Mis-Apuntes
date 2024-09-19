
Para poder abrir el puerto 3389 primero necesitamos tener acceso a la maquina victima con permisos de administrador

Como podemos ver hemos obtenido acceso desde la vulnerabilidad badblue y ya tenemos los privilegios de admininistrador
![[Pasted image 20240409081229.png]]

Ahora saldremos de la sesion de meterpreter y seleccionaremos el siguiente modulo 
`post/windows/manage/enable_rdp´
![[Pasted image 20240409081327.png]]

Configuramos el modulo
![[Pasted image 20240409081446.png]]

Y al ejecutarlo podemos ver que nos indica que ya esta habilitado el puerto
![[Pasted image 20240409081535.png]]

Lo comprobamos con un escaneo del puerto
![[Pasted image 20240409081800.png]]

Ahora para probar el acceso utilizaremos xfreerdp pero antes necesitaremos tener el acceso de un usuario, nosotros cambiaremos la password de admin aun que no es una practica recomendable ya que cuando la victima intentase acceder descubriria que ha sido hackeado
![[Pasted image 20240409082101.png]]

Ahora utilizando la herramienta xfreerdp obtendremos acceso remoto
xfreerdp /u:administrator /p:hack_123321 /v:10.2.29.0
![[Pasted image 20240409082242.png]]
