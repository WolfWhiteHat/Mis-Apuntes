Primero necesitamos obtener acceso al sistema de destino con privilegios elevados
![[Pasted image 20240513074416.png]]

Una vez obtenida la sesión saldremos guardandola y cargaremos el siguiente modulo
`exploit/windows/local/persistence_service`
![[Pasted image 20240513074541.png]]

Lo configuramos
![[Pasted image 20240513074620.png]]

Y lo ejecutamos, como podemos ver ya hemos obtenido acceso al sistema
![[Pasted image 20240513074702.png]]

Como se puede ver en la siguiente imagen tenemos dos sesiones abiertas, este modulo ejecuta una carga util en el sistema de destino el cual se va ejecutando por defecto cada 5 segundos si no lo cambiamos, en caso de perdida ejecutando un oyente por el mismo puertos que en el modulo recuperariamos acceso al sistema
![[Pasted image 20240513074839.png]]

Matamos las sesiones
![[Pasted image 20240513074925.png]]

Cargamos el modulo `multi/handle` y lo configuramos con nuestra IP y el mismo puerto que el modulo de persistencia
![[Pasted image 20240513075206.png]]

Como podemos ver pudimos recuperar nuestra sesión después de matar todas las sesiones
![[Pasted image 20240513082804.png]]


