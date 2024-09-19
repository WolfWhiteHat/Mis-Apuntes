Primero obtenemos una sesion shell basica
![[Pasted image 20240327122856.png]]

Salimos de la sesión y comprobamos que esta guardada
![[Pasted image 20240327123017.png]]


Tenemos dos formas de convertir la sesion, la primera es ejecutando el siguiente modulo
`post(multi/manage/shell_to_meterptreter)`
![[Pasted image 20240327123333.png]]


Como podemos ver ya tenemos la sesion de meterpreter creada
![[Pasted image 20240327123416.png]]


Y la otra manera es ejecutando una opcion del comando sessions
```
sessions -u 4 -i 2
```
![[Pasted image 20240327123528.png]]

En esta captura podemos ver que tenemos las dos sesiones de meterpreter creadas de dos formas diferentes
![[Pasted image 20240327123639.png]]



------------------------------

Otra alternativa que tenemos para otener una sesion de meterpreter una vez obtenida la sesion shell es usando el siguiente comando
`sessions -u <sesion>`


Luego para volver a una sesion shell dentro de meterpreter podremos usar el siguiente comando
`/bin/shell -i`