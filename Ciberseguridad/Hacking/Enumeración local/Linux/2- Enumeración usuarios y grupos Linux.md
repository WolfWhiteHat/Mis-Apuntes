# Listar usuario actual
`getuid`
![[Pasted image 20240507081648.png]]

`whoami`
![[Pasted image 20240507081713.png]]

# Listar grupos
`groups`
![[Pasted image 20240507081743.png]]

# Listar usuarios dentro de un grupo
`groups root`
![[Pasted image 20240507081802.png]]

# Listar usuarios
`cat /etc/passwd`
![[Pasted image 20240507081836.png]]

`ls /home`
![[Pasted image 20240507081945.png]]

# Listar solo usuarios con login
`cat /etc/passwd | grep -v /nologin
![[Pasted image 20240507081521.png]]

# Mostrar ultimos inicio de sesion legitimos
`last`
![[Pasted image 20240507082654.png]]

# Mostrar log ultimos inicios de sesion
`lastlog`
![[Pasted image 20240507082708.png]]
