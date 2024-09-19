# Como enumerar procesos de windows
```bash
ps
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101300.png]]
O también podemos enumerar procesos con el comando net start:
![[Mis apuntes/ANEXOS/Pasted image 20230801101455.png]]
# Conocer PID de un proceso
```bash
pgrep explorer.exe
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101332.png]]
O también podemos ver los PID de todos los procesos con el siguiente comando:
```bash
wmic ervice list brief
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101552.png]]
# Migrar a un proceso
```bash
migrate 2176
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101356.png]]
# Enumerar tareas programadas
```bash
tasklist /SVC
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101626.png]]
O también tenemos este otro comando:
```bash
schtasks /query /fo LIST
```
![[Mis apuntes/ANEXOS/Pasted image 20230801101703.png]]
