xfreerdp es un cliente de escritorio remoto X11 que forma parte del proyecto FreeRDP. Permite conectarse a servidores que utilizan el protocolo RDP (Remote Desktop Protocol), como los que vienen integrados en muchas ediciones de Windows

Para poder utilizar esta herramienta necesitaremos las credenciales de un usuario del sistema que tenga acceso al protocolo RDP

Una vez obtenemos las credenciales con la herramienta xfreerdp probaremos a acceder al equipo victima
```Bash
xfreerdp /u:administrator /p:qwertyuiop /v:10.2.28.248:3333
```
![[Pasted image 20240308100431.png]]

Como podremos ver se nos abrirá una pantalla con la conexión en remoto
![[Pasted image 20240308100451.png]]