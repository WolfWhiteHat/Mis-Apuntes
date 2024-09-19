
Para conseguir persistencia utilizando la clave de SSH primero necesitaremos acceso a la maquina victima
![[Pasted image 20240415073232.png]]

Para poder obtener persistencia primero necesitaremos obtener los privilegios de root, para ello realizaremos una escalada de privilegios, en esta maquina hay una vulnerabilidad de chkrootkit

Antes de ejecutar el modulo actualizaremos la sesion a meterpreter
![[Pasted image 20240415073707.png]]

Cargamos el modulo de chkrootkit
![[Pasted image 20240415074152.png]]
![[Pasted image 20240415074232.png]]

Ejecutamos el modulo y obtenemos una sesion con privilegios de root
![[Pasted image 20240415074358.png]]

Actualizamos la sesión con los privilegios de root
![[Pasted image 20240415075120.png]]

Ahora utilizaremos el siguiente modulo para obtener la clave privada
`post/linux/manage/sshkey_persistence`
![[Pasted image 20240415075442.png]]

Ejecutamos el modulo
![[Pasted image 20240415075506.png]]

Como podemos ver en la siguiente captura hemos podido obtener la clave privada
![[Pasted image 20240415075555.png]]



Creamos un fichero con el nombre ssh_key y adjuntamos la clave
![[Pasted image 20240415082110.png]]
![[Pasted image 20240415082054.png]]

Otorgamos permisos al archivo
![[Pasted image 20240415081245.png]]

Ahora accedemos con ssh utilizando el archivo con la clave privada
![[Pasted image 20240415082018.png]]
