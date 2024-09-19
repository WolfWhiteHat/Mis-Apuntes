`chkrootkit` es una herramienta de seguridad de código abierto diseñada para detectar rootkits en sistemas basados en Unix, como Linux. Un rootkit es un tipo de software malicioso diseñado para ocultar la presencia de ciertos procesos o programas, así como para mantener el acceso no autorizado al sistema. Los rootkits son una herramienta comúnmente utilizada por los atacantes para mantener el control de un sistema comprometido de manera encubierta.

`chkrootkit` busca patrones específicos que podrían indicar la presencia de rootkits en el sistema. Examina archivos y procesos en busca de signos de actividad maliciosa. Si detecta algo sospechoso, emite una alerta para que el administrador del sistema pueda investigar más a fondo.

La vulnerabilidad que vamos a explotar ahora solo funciona para versiones 0.5.0

Para poder ver que versión esta ejecutando podemos utilizar el comando
```
chkrootkit -V
```

El modulo que utilizaremos es el siguiente
`exploit/unix/local/chkrootkit`


Con la sesion ya obtenida como podremos ver en la siguiente imagen accederemos a la sesion y verificaremos la version de chkrootkit, es importante tener la sesion de meterpreter, si no el exploit no funcionara
![[Pasted image 20240410144146.png]]

Ahora revisando los procesos activos vemos revisaremos el `/bin/check-down`el cual se esta ejecutando en /bin/bash
![[Pasted image 20240410143329.png]]

Ahora revisamos la version de rootkit
![[Pasted image 20240410143406.png]]

Buscamos la vulnerabilidad
![[Pasted image 20240410143510.png]]

Preparamos el exploit con el payload
![[Pasted image 20240410144250.png]]

Como podemos ver ya hemos obtenido los permisos de root
![[Pasted image 20240410144351.png]]