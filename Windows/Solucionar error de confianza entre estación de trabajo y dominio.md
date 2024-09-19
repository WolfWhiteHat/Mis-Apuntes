
Dentro de una sesión de PowerShell con permisos ejecutamos el siguiente comando
```
Test-ComputerSecureChannel –verbose
```
![[Captura 1.png]]

La respuesta sera algo asi
```
False  
VERBOSE: The Secure channel between the local computer and the domain dominio.local is broken.
```

Para solucionarlo escribiremos lo siguiente
Aparece una ventana donde introducir un usuario y contraseña con permisos en el dominio, de esta forma repararemos la relación.
```
Test-ComputerSecureChannel –Repair –Credential (Get-Credential)
```
![[Pasted image 20240918121016.png]]

Volvemos a comprobar la relación
```
Test-ComputerSecureChannel –verbose
```
![[Captura 3.png]]

Si la salida aparece así el problema estaría resuelto
```
True  
VERBOSE: The Secure channel between the local computer and the domain dominio.local is in good condition.
```
![[Captura 4.png]]

En el caso de que no funcione iremos al servidor y ejecutaremos el siguiente comando
```
netdom resetpwd /s:<NombrePC> /UserD:<Dominio\Administrador> /PasswordD:<Contraseña>
```
