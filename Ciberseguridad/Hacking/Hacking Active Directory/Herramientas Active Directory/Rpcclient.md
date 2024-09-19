Es una herramienta que permite realizar llamadas a procedimientos remotos (RPC) en un servidor SAMBA. Puede utilizarse para realizar una variedad de operaciones en un servidor SAMBA, como enumerar usuarios, grupos, recursos compartidos, entre otros.


# Comandos
![[Pasted image 20240304140553.png|1500]]

# Conexión remota
```Bash
rpcclient -U "" -N [IP]
```
![[Pasted image 20240304143343.png]]

# Información del SO
```Bash
srvinfo
```
![[Pasted image 20240304165952.png]]

# Enumerar usuarios
```Bash
enumdomusers
```
![[Pasted image 20240304170021.png]]

# Obtener SID
```Bash
lookupnames admin
```
![[Pasted image 20240304170101.png]]

# Listar grupos
```Bash
enumdomgroups
```
![[Pasted image 20240304172940.png]]