Windows PrivescCheck escanea el sistema en busca de diferentes configuraciones, permisos, vulnerabilidades o servicios inseguros que podrían ser explotados para lograr una escalada de privilegios.

```bash
https://github.com/itm4n/PrivescCheck
```

-------------------------

Somos el usuario student:
![[Mis apuntes/ANEXOS/Pasted image 20230801084619.png]]

Y lo ejecutamos con este parámetro:
```bash
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
```

Y en este caso nos encuentra unas credenciales:
![[Mis apuntes/ANEXOS/Pasted image 20230801085233.png]]

Ahora para autenticarnos como el usuario administrador, ejecutaremos el comando 
```Shell
runas.exe /user:administrator cmd
```
![[Mis apuntes/ANEXOS/Pasted image 20230801085456.png]]

-----

# Acceder con privilegios elevados con PSexec
[[Psexec]]