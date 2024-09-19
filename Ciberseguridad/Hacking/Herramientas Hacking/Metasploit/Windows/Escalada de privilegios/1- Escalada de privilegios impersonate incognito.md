El siguiente modulo que vamos a utilizar viene implantado directamente en meterpreter, para ello obtenemos una sesion y comprobamos que privilegios tenemos, para poder realizar esta escalada de privilegios es necesario disponer de `ImpersonatePrivilege`
![[Pasted image 20240403085653.png]]

Una vez lo verificamos cargamos el modulo
load_incognito
![[Pasted image 20240403085851.png]]

Ahora listamos los tokens
list_tokens -u
![[Pasted image 20240403090025.png]]


Ahora para suplantar el token que queremos tendríamos que cargar el siguiente comando
impersonate_token "ATTACKDEFENSE\Administrator"
![[Pasted image 20240403090252.png]]


Ahora solo faltaria migrar el proceso a explorer.exe
![[Pasted image 20240403090408.png]]

Y ya podriamos obtener los hashes
![[Pasted image 20240403090500.png]]