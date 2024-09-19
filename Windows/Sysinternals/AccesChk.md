Es una herramienta de línea de comandos de Sysinternals que muestra los derechos de acceso asignados a usuarios, grupos y cuentas de servicio para archivos, directorios, claves del registro y otros objetos del sistema en sistemas Windows. Es especialmente útil para auditar y verificar los permisos de seguridad en un sistema o en recursos específicos.
AccessChk muestra los derechos de acceso asignados a usuarios y grupos para archivos, directorios, claves del registro y otros objetos del sistema. Puede ser utilizado para auditar y verificar los permisos de seguridad en un sistema Windows. AccessChk muestra los derechos de acceso efectivos, es decir, los derechos de acceso que realmente se aplican a un usuario o grupo específico, teniendo en cuenta la herencia y las reglas de permisos.


# Parametros AccesChk
- `-accepteula`: Acepta la licencia de usuario final (EULA) de Sysinternals sin solicitar confirmación.
- `-c`: Muestra únicamente los nombres de los objetos afectados por los derechos de acceso, sin detalles adicionales.
- `-d`: Muestra únicamente los objetos que deniegan el acceso al usuario o grupo especificado.
- `-e`: Muestra los derechos de acceso efectivos para el usuario o grupo especificado.
- `-f`: Muestra únicamente los objetos que permiten el acceso al usuario o grupo especificado.
- `-k`: Realiza la búsqueda de cadenas de texto en lugar de nombres de objetos.
- `-l`: Incluye el nombre del objeto, la descripción y la ruta completa en la salida.
- `-n`: No sigue los enlaces simbólicos al enumerar los objetos del sistema.
- `-q`: No muestra mensajes de encabezado en la salida.
- `-r`: Enumera recursivamente los subdirectorios o subclaves del registro.
- `-s`: Enumera el contenido de subdirectorios de directorios especificados.
- `-u`: Muestra únicamente los objetos que no tienen asignados derechos de acceso al usuario o grupo especificado.
- `-v`: Muestra detalles adicionales sobre los derechos de acceso, como el tipo de objeto y la identificación del proceso que concedió el acceso.
- `-w`: Muestra la salida en formato ancho para facilitar la lectura.

# Instalar acceschk
```
wget https://download.sysinternals.com/files/AccessChk.zip
```
![[Pasted image 20240724124729.png]]

Lo descomprimimos
```
unzip AccessChk.zip
```
![[Pasted image 20240724124806.png]]

# Revisar permisos usuario
Ahora utilizaremos la herramineta `accesschk.exe` de sysinternal para revisar los permisos del sistema
```
C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc
```
![[Pasted image 20240718135141.png]]
- **C:\PrivEsc\accesschk.exe**: Es la ruta completa del ejecutable `accesschk.exe`. Este programa es una herramienta de línea de comandos desarrollada por Sysinternals (ahora parte de Microsoft) que se utiliza para verificar los permisos de acceso a objetos del sistema, como archivos, directorios, claves de registro, etc.
- **/accepteula**: Es un parámetro que indica que el usuario acepta el acuerdo de licencia de usuario final (EULA, End User License Agreement) de Sysinternals automáticamente sin necesidad de confirmación manual.
- **-uwcqv**: Estos son los parámetros que se pasan al programa `accesschk.exe`, y tienen los siguientes significados:
    - **-u**: Elimina posibles errores en la salida
    - **-w**: Mostrar solo objetos con acceso de escritura
    - **-c**: Nombre es un servicio especifico de Windows
    - **-q**: Omitir Banner
    - **-v**: Muestra información detallada (Verbose mode, modo detallado).
- **user**: Es el nombre del usuario para el cual se están consultando los permisos de acceso en el objeto especificado por el siguiente parámetro.
- **daclsvc**: Es el nombre del objeto (archivo, directorio, etc.) para el cual se están verificando los permisos de acceso para el usuario especificado (`user`).

# Revisar permisos directorio
```
accesschk.exe -uwqv <usuario> <directorio>
```

# Mostrar todos los archivos con escritura
```
accesschk -wu usuario C:\
```
Utiliza `-w` para permisos de escritura y `-u` seguido del nombre del usuario para especificar el usuario.