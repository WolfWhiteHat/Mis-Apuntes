Es una herramienta de línea de comandos que permite a los usuarios acceder a recursos compartidos de archivos y realizar diversas operaciones en ellos, como listar archivos, transferir archivos, etc. Es similar al cliente SMB utilizado en sistemas Windows para acceder a recursos compartidos en una red.

# Comandos SMBCLIENT
![[Pasted image 20240304140057.png|1500]]

## Ejecutar comandos con SMBCLIENT
```Bash
smbmap -H [IP] -u 'usuario' -p 'password'
```

## Listar recurso compartido con NULL Sesion
```Bash
smbclient -L 10.129.95.187 -N
```
![[Pasted image 20240522094443.png]]

## Conexión cliente sin contraseña
```Bash
smbclient -N 10.129.95.187 
```
![[Pasted image 20240522094751.png]]

También podemos subir archivos con el comando put, por ejemplo voy a subir un documento txt:
![[Mis apuntes/ANEXOS/Pasted image 20230420110901.png]]

Si lo quisiera descargar utilizaría el comando get:
![[Mis apuntes/ANEXOS/Pasted image 20230420111148.png]]

## Conexión cliente
```Bash
smbclient //[IP]/ruta -U Usuario

```
![[Pasted image 20240304184703.png]]

