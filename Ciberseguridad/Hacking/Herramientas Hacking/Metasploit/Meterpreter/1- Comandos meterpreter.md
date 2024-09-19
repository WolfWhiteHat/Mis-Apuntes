Meterpreter es una herramienta de post-explotación utilizada en el campo de la ciberseguridad. Es parte del Framework Metasploit, que es una plataforma de pruebas de penetración y desarrollo de exploits. Meterpreter se utiliza específicamente para obtener acceso persistente y control total sobre un sistema comprometido después de haberse explotado con éxito una vulnerabilidad.

# Comandos Meterpreter

## Comandos básicos
- `sysinfo`: Muestra información detallada sobre el sistema comprometido, como el sistema operativo, la arquitectura del procesador y la versión del kernel.
- `getuid`: Proporciona información sobre el usuario actualmente autenticado
- `getsystem`: Intenta obtener privilegios de sistema en el sistema comprometido.
- `getpid`: Muestra el identificador de proceso (PID) del proceso Meterpreter en el sistema comprometido.
- `getdesktop`: Captura una captura de pantalla del escritorio actual del usuario en el sistema comprometido y la descarga al sistema del atacante.
- `ps`: Muestra una lista de los procesos en ejecución en el sistema comprometido, incluidos sus identificadores de proceso (PID) y nombres.
- `pwd`: Muestra el directorio de trabajo actual.
- `help`: Muestra la lista de comandos disponibles.
- `cd`: Cambia el direcctorio de trabajo
- `ls`: Lista los archivos
- `shell`: Abre una shell interactiva en el sistema comprometido, lo que permite al atacante ejecutar comandos como si estuviera directamente en el sistema.
- `download`: Descarga un archivo desde el sistema comprometido al sistema del atacante.
- `upload`: Sube un archivo desde el sistema del atacante al sistema comprometido.
- `execute`: Ejecuta un archivo en el sistema objetivo
- `.\`: Ejecutar programa

## Comandos de red
- `portfwd` - Reenvía puertos en el sistema objetivo.
-  `portscan` - Escanea puertos en un rango especificado.
-  `route` - Muestra o modifica la tabla de enrutamiento del sistema.

## Comandos manipular archivos
- `mkdir` - Crea un nuevo directorio en el sistema objetivo.
- `rm` - Elimina archivos en el sistema objetivo.
- `rmdir` - Elimina directorios en el sistema objetivo.
- `edit` - Edita un archivo en el sistema objetivo utilizando un editor de texto integrado.
- `download` - Descarga un archivo del sistema objetivo al sistema local.
- `clearev`: Borra los registros de eventos del sistema comprometido para eliminar rastros de actividad.
## Escalada de privilegios
- `getsystem` - Intenta obtener privilegios de sistema en el sistema objetivo.
- `run` - Ejecuta un comando en el sistema objetivo.
- `getprivs` - Muestra los privilegios disponibles en el sistema objetivo.

## Explotación y post-explotación
- `hashdump` - Extrae contraseñas en forma de hashes almacenadas en el sistema.
- `keyscan_start` - Inicia la captura de pulsaciones de teclas en el sistema.
- `screenshot` - Captura una captura de pantalla del escritorio del sistema objetivo.
- `webcam_list` - Lista las cámaras web disponibles en el sistema objetivo.
- `migrate` - Mueve el proceso Meterpreter a otro proceso en el sistema.
- `resource`: Ejecuta un script almacenado en un archivo externo. 


# Modulos Metasploit

## Modulo exploit kernel
post/multi/recon/local_exploit_suggester

# Migrar sesion en Meterpreter

Revisamos todos los procesos que se estan ejecutando
ps
![[Pasted image 20240326083406.png]]

pgrep explorer
migrate ID
![[Pasted image 20240326083011.png]]

buscar tarea y migrar
search -f
pgrep

Otra forma de migrar automaticamente una sesion es usando el siguiente modulo
run post/windows/manage/migrate

# Obtener sesion bash
![[Pasted image 20240314083548.png]]

