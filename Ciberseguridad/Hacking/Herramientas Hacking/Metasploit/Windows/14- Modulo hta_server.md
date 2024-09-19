Este módulo aloja una aplicación HTML (HTA) que cuando se abre ejecutar una carga útil a través de Powershell. Cuando un usuario navega al archivo HTA IE les solicitará dos veces antes de que se ejecute la carga útil.

Buscamos el modulo y lo cargamos
![[Pasted image 20240509111453.png]]

Lo ejecutamos
![[Pasted image 20240509111458.png]]

En la maquina victima ejecutamos el siguiente comando en powershell o en un navegador, cuando lo ejecutamos aparentemente no hace nada pero si nos volvemos a la maquina podemos ver como hemos obtenido una sesion de meterpreter por tener cargado el payload
![[Pasted image 20240509111500.png]]

Como vemos después de ejecutarlo nos indica que hemos obtenido acceso
![[Pasted image 20240509111501.png]]

Revisamos las sesiones y comprobamos el acceso a la maquina victima
![[Pasted image 20240509111540.png]]