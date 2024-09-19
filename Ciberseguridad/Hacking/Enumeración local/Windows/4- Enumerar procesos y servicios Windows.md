
# Listar todos los procesos
![[Pasted image 20240506143700.png]]

# Listar proceso y migrar
![[Pasted image 20240506143703.png]]

# Listar servicios ejecutando en Windows
```
net start 
```
![[Pasted image 20240506143704.png]]

# Listar servicios instalados
```
wmic service list brief
```
![[Pasted image 20240506143704 1.png]]

# Listar procesos en ejecución 
```
tasklist /SVC
```
![[Pasted image 20240506143705.png]]

# Enumerar tareas programas
```
schtasks /query /fo LIST /v
```
![[Pasted image 20240506143706.png]]