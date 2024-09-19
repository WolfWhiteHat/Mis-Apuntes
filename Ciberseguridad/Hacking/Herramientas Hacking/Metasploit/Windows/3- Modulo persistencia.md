Con el sigueinte modulo vamos a obtener persistencia
`exploit/windows/local/persistence_service`

Primero tenemos que obtener una sesión con privilegios en la maquina victima, para ello utilizaremos el modulo previamente indicado
![[Pasted image 20240404090312.png]]

Como podemos ver ya hemos obtenido persistencia
![[Pasted image 20240404090338.png]]

Ahora cerraremos las sesiones
![[Pasted image 20240404090452.png]]

Seleccionamos el modulo `multi/handler`
![[Pasted image 20240404090525.png]]

Preparamos la carga
![[Pasted image 20240404090716.png]]

Y ejecutamos el modulo, como podemos ver aun que se cierre la sesion continuamos manteniendo acceso al equipo
![[Pasted image 20240404090802.png]]


