Puertos escaneados
![[Pasted image 20240702112151.png]]
![[Pasted image 20240702112224.png]]

Enumeramos el servicio SMB y encontramos la siguiente información
![[Pasted image 20240702142014.png]]
![[Pasted image 20240702142113.png]]
![[Pasted image 20240702142154.png]]
![[Pasted image 20240702142224.png]]
![[Pasted image 20240702142255.png]]
### Grupos y Usuarios

- **Usuarios Unix**:
    - `ubuntu`
    - `auditor`
    - `dbadmin`
- **Grupos BUILTIN**:
    - Administrators
    - Users
    - Guests
    - Power Users
    - Account Operators
    - Server Operators
    - Print Operators


Accedemos por ftp y nos descargamos el  fichero de updates que al leerlo nos muestra lo siguiente
![[Pasted image 20240702143043.png]]

Con los usuarios obtenidos realizamos un ataque de fuerza bruta y obtenemos la password de dbadmin
![[Pasted image 20240702145751.png]]

Probamos ha acceder y estamos denttrp
![[Pasted image 20240702150047.png]]

Obtenemos la flag de auditor
![[Pasted image 20240702150143.png]]

Encontramos una posible password para el ususario de la base de datos
![[Pasted image 20240702152027.png]]

Probamos las credenciales y estamos dentro de la base de datos
![[Pasted image 20240702152142.png]]

Encontramos los usuarios en la base de datos
![[Pasted image 20240702152317.png]]