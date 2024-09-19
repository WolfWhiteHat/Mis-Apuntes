Sysmon, o System Monitor, es una herramienta de Sysinternals diseñada para monitorear y registrar la actividad del sistema en sistemas Windows. Sysmon registra eventos relacionados con procesos que se inician, cambios en el sistema de archivos, cambios en el registro, conexiones de red y mucho más. Está diseñado para ayudar en la detección de amenazas y en la respuesta a incidentes de seguridad al proporcionar un registro detallado de la actividad del sistema.

# Parametros Sysmon
- `-accepteula`: Acepta la licencia de usuario final (EULA) de Sysmon sin solicitar confirmación.
- `-c <config file>`: Especifica el archivo de configuración XML que Sysmon debe usar para personalizar su comportamiento.
- `-h`: Muestra la ayuda de línea de comandos.
- `-i`: Instala Sysmon como un servicio del sistema.
- `-l`: Muestra la configuración actual de Sysmon.
- `-n`: No configura el servicio del sistema para que se inicie automáticamente en el arranque.
- `-m [processes [processes ...]]`: Filtra los eventos de creación de procesos para los procesos especificados. Pueden ser nombres de procesos, rutas de archivos o rutas de carpetas.
- `-r`: Desinstala Sysmon y elimina su servicio del sistema.
- `-s`: Actualiza el servicio de Sysmon a la versión más reciente.
- `-u`: Desinstala Sysmon pero conserva su configuración existente.

# Instalar Sysmon
```
syson.exe -i
```
![[Pasted image 20240918095007.png]]

# Verificar que Sysmon esta ejecutandose
```
sc query SysmonDrv
```
![[Pasted image 20240918095027.png]]