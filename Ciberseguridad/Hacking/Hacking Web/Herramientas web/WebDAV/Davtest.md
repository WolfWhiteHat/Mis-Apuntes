DavTest verifica si webdav se encuentra activo en los servidores para subir archivos ejecutables, para luego (opcionalmente) subir archivos que permitan la ejecución de comandos u otras acciones. Está pensado para que pentesters determinen de forma rápida y fácil si el servicio DAV es explotable.
### Comandos

![[Pasted image 20240307120039.png]]

### Ejemplo
davtest -url http://10.2.20.83/webdav
![[Pasted image 20240307121012.png]]


davtest -auth bob:password_123321 -url http://10.2.20.83/webdav
![[Pasted image 20240307121455.png]]