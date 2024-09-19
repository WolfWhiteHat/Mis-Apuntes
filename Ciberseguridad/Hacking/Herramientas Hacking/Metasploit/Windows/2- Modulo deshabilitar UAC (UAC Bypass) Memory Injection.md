El siguiente modulo se utiliza para deshabilitar UAC del sistema y poder obtener los privilegios mas altos del sistema
```
exploit/windows/local/bypassuac_injection
```


Primero necesitamos obtener una sesion de meterpreter de la maquina victima, en la siguiente imagen vemos como tenemos ya la sesion con los permisos
sysinfo
getuid
![[Pasted image 20240402141722.png]]
![[Pasted image 20240402141748.png]]

Intentamos obtener acceso desde meterpreter pero no obtenemos el acceso
getsystem
![[Pasted image 20240402141848.png]]

Accedemos a una sesion shell para verificar que usuarios tienen acceso administrador
![[Pasted image 20240402142035.png]]


Ahora cargaremos el siguiente modulo y lo configuraremos, en la segunda imagen hemos configurado el parametro TARGET ya que hay que seleccionar la arquitectura correcta
![[Pasted image 20240402142442.png]]
![[Pasted image 20240402142810.png]]

Una vez obtenemos acceso de meterpreter ejecutaremos el siguiente comando `getsystem` con la diferencia que ahora si que obtendremos los permisos ya que previamente habremos deshabilitado UAC.
![[Pasted image 20240402143231.png]]

Para finalizar migraremos la sesion
ps -S lsass.exe
migrate 684
![[Pasted image 20240402143441.png]]