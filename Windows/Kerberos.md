# Obtener información usuario Kerberos krbtgt
```Powershell
Get-AdUser krbtgt -property created, passwordlastset, enabled
```
![[Pasted image 20240918094400.png]]

Por razones de seguridad y para contrarrestar un ataque del tipo Golden Ticket Attack, es necesario cambiar periódicamente la contraseña de la cuenta de dominio krbtgt (una vez al año y cuando cualquier administrador de dominio deja su empresa). Debe cambiar la contraseña dos veces (con un retraso suficiente para realizar la replicación en todo el dominio), porque la contraseña actual y anterior de la cuenta krbtgt se almacena en el dominio. Incluso si los atacantes emitieron el Golden Ticket con un largo período de validez, después de cambiar la contraseña krbtgt, este ticket se volverá inútil.

# Restablecer password krbtgt
![[Pasted image 20240430121444.png]]

# Restablecer servicio Kerberos
![[Pasted image 20240430121731.png]]

O podemos utilizar el siguiente script
```PowerShell
$DCs=Get-ADDomainController
Get-Service KDC -ComputerName $DCs | Restart-Service
```
![[Pasted image 20240918121245.png]]

# Enlace interes
https://www.tarlogic.com/es/blog/como-funciona-kerberos/
