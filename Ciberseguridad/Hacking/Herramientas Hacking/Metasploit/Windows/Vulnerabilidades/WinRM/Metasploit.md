Vamos a explotar el protocolo WInRM, para ello hay que tener en cuenta que el escaneo no puede ser el comun ya que no entra dentro de los 1000 puertos mas comunes, para ello realizaremos el siguiente comandos
nmap -sV -p 5985 10.2.28.238
![[Pasted image 20240308120426.png]]

Una vez descubierto que la maquina victima tiene el servicio activo intentaremos explotarlo con metasploit, para ello tenemos el siguiente exploit
Seleccionamos el modulo y lo configuramos para realizar un ataque de fuerza bruta auxiliary/scanner/winrm/winrm_login 
![[Pasted image 20240308120815.png]]
![[Pasted image 20240308120844.png]]

Una vez ejecutado el auxiliar podemos ver que hemos obtenido la contraseña del usuario administrador
![[Pasted image 20240308121157.png]]


Verificamos el metodo de autentificación con el siguiente auxiliar
auxiliary/scanner/winrm/winrm_lauth_methods
![[Pasted image 20240308121404.png]]


Una vez verificado que podemos acceder por via winrm ejecutaremos el siguiente exploit para conectarnos desde cmd y lo preparamos
use auxiliary/scanner/winrm/winrm_cmd
![[Pasted image 20240308121926.png]]

Ejecutamos el exploit y como vemos a realizado la accion que solicitabamos, es decir que mostrara que usuario somos en el sistema
![[Pasted image 20240308122014.png]]

Ahora ejecutaremos un exploit para hacer un revershell, para ello seleccionaremos el siguiente exploit
exploit/windows/winrm/winrm_script_exec
![[Pasted image 20240308122306.png]]

Como vemos ya nos ha asignado un payload por defecto para realizar un reverse_tcp

Configuramos el exploit
![[Pasted image 20240308122353.png]]
![[Pasted image 20240308122419.png]]

Y lo ejecutamos
![[Pasted image 20240308122533.png]]
![[Pasted image 20240308122625.png]]

Como podemos ver ya hemos obtenido acceso a la maquina victima

Ahora solo falta buscar la bandera
![[Pasted image 20240308122746.png]]


