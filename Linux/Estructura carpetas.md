![[Pasted image 20231113074343.png]]

# **/bin – Binarios**

El ‘/bin’ contiene directamente los archivos ejecutables de muchos comandos básicos del shell como ls, cp, cd, etc. La mayoría de los programas están en formato binario aquí y son accesibles para todos los usuarios del sistema Linux.

# **/dev – Archivos de dispositivos**

Este directorio sólo contiene archivos especiales, incluidos los relativos a los dispositivos. Son archivos virtuales, no están físicamente en el disco.

Algunos ejemplos interesantes de estos archivos son:

`/dev/null`
puede ser enviado para destruir cualquier archivo o cadena

`/dev/zero`
contiene una secuencia infinita de 0

`/dev/random`
contiene una secuencia infinita de valores aleatorios

`/dev/shm`
Es un directorio especial que se utiliza para almacenar archivos temporales en la memoria RAM
# **/etc – Archivos de configuración**

El directorio /etc contiene los archivos de configuración principales del sistema, utilizados principalmente por el administrador y los servicios, como el archivo de contraseñas y los archivos de red.

Si necesitas hacer cambios en la configuración del sistema (por ejemplo, cambiar el nombre del host), aquí es donde encontrarás los archivos respectivos.

`/etc/passwd`
Información de los usuarios

`/etc/shadow`
Almacena las contraseñas de los usuarios (solo puede acceder sudo)

`/etc/*issue`
Contiene información que se muestra antes de iniciar sesión en un sistema a través de la terminal o una conexión de red. Por ejemplo, en distribuciones como Ubuntu, este archivo puede contener información sobre la versión del sistema operativo y quizás algunos detalles adicionales.

`/etc/*release`
Contiene información sobre la versión específica de la distribución de Linux que estás utilizando, como el nombre de la distribución, la versión y alguna otra información relevante.

`/etc/shells`
Almacena todos los shells instalados

`/etc/cron*`
Ubica todos los directorios con las tareas programadas

`/etc/sudoers.d`
Gestiona que usuarios pueden ejecutar los comandos como sudo
![[Pasted image 20240604100124.png]]
# **/usr – Binarios de usuario y datos de programas**

En ‘/usr’ van todos los archivos ejecutables, las bibliotecas, el código fuente de la mayoría de los programas del sistema. Por esta razón, la mayoría de los archivos que contiene es de sólo lectura (para el usuario normal)

- ‘/usr/bin’ contiene los comandos básicos del usuario
- /usr/sbin’ contiene comandos adicionales para el administrador
- ‘/usr/lib’ contiene las bibliotecas del sistema
- ‘/usr/share’ contiene la documentación o común a todas las bibliotecas, por ejemplo ‘/usr/share/man’ contiene el texto de la página man

# **/home – Datos personales del usuario**

El directorio home contiene los directorios personales de los usuarios. El directorio personal contiene los datos del usuario y los archivos de configuración específicos del usuario. Como usuario, pondrás tus archivos personales, notas, programas, etc. en tu directorio personal.

Cuando creas un usuario en tu sistema Linuxes una práctica general crear un directorio personal para el usuario. Supongamos que tu sistema Linux tiene dos usuarios, Alice y Bob. Ellos tendrán un directorio personal en las ubicaciones /home/alice y /home/bob.

Ten en cuenta que Bob no tendrá acceso a /home/alice y viceversa. Esto tiene sentido porque sólo el usuario debe tener acceso a su casa. Puedes leer sobre los permisos de archivos en Linuxpara saber más sobre este tema.

# **/lib – Bibliotecas compartidas**

Las bibliotecas son básicamente códigos que pueden ser utilizados por los binarios ejecutables. El directorio /lib contiene las bibliotecas que necesitan los binarios de los directorios /bin y /sbin.

Las bibliotecas que necesitan los binarios en /usr/bin y /usr/sbin se encuentran en el directorio /usr/lib.

# **/sbin – Binarios del sistema**

Es similar al directorio /bin. La única diferencia es que contiene los binarios que sólo pueden ser ejecutados por root o un usuario sudo. Puedes pensar en la ‘s’ de ‘sbin’ como super o sudo.

# **/tmp – Archivos temporales**

Como su nombre indica, este directorio contiene archivos temporales. Muchas aplicaciones utilizan este directorio para almacenar archivos temporales. Incluso usted puede utilizar el directorio para almacenar archivos temporales.

Pero ten en cuenta que los contenidos de los directorios /tmp se borran cuando su sistema se reinicia. Algunos sistemas Linux también eliminan los archivos antiguos automáticamente, así que no almacene nada importante aquí.

# **/var – Archivos de datos variables**

Var, abreviatura de variable, es el lugar donde los programas almacenan la información en tiempo de ejecución, como el registro del sistema, el seguimiento de los usuarios, las cachés y otros archivos que los programas del sistema crean y gestionan.

Los archivos que se almacenan aquí NO se limpian automáticamente y, por lo tanto, es un buen lugar para que los administradores del sistema busquen información sobre el comportamiento de su sistema. Por ejemplo, si quieres comprobar el historial de inicio de sesión en tu sistema Linux sólo tienes que comprobar el contenido del archivo en /var/log/wtmp.

# **/boot – Archivos de arranque**

El directorio ‘/boot’ contiene los archivos del kernel y la imagen de arranque, además de LILO y Grub. Suele ser recomendable que el directorio resida en una partición al principio del disco.

# **/proc – Archivos del proceso y del núcleo**

El directorio ‘/proc’ contiene la información sobre los procesos que se están ejecutando y los parámetros del kernel. El contenido del directorio proc es utilizado por una serie de herramientas para obtener información del sistema en tiempo de ejecución.

- **`/proc/net/tcp`**: Contiene información sobre las conexiones TCP activas en el sistema, incluyendo direcciones locales y remotas, puertos, estados de conexión y más. Se utiliza para monitorear y diagnosticar la actividad de la red.
- **`/proc/[pid]/cmdline`**: Contiene la línea de comando que se usó para iniciar el proceso. Los argumentos de la línea de comando se almacenan como una cadena de texto única, con cada argumento separado por un carácter nulo (`\0`).
- **`/proc/[pid]/status`**: Proporciona información diversa sobre el proceso, incluyendo su estado, ID del proceso (PID), ID del padre (PPID), ID del grupo (GID), cantidad de memoria utilizada y más. Este archivo es más fácil de leer para los humanos comparado con otros archivos en `/proc`, como `/proc/[pid]/stat`.
- **`/proc/[pid]/fd/`**: Es un directorio que contiene enlaces simbólicos (symlinks) a los descriptores de archivos abiertos por el proceso. Cada enlace simbólico está nombrado con el número del descriptor de archivo y apunta al archivo o recurso que está siendo accedido por el descriptor. Por ejemplo, `0` es estándar de entrada (stdin), `1` es estándar de salida (stdout), y `2` es estándar de error (stderr).
- **`/proc/[pid]/environ`**: Contiene las variables de entorno que estaban configuradas para el proceso en el momento en que fue iniciado. Las variables de entorno están separadas por caracteres nulos (`\0`), similar a cómo se representan los argumentos en `/proc/[pid]/cmdline`.
- **`/proc/[pid]/cwd`**: Es un enlace simbólico que apunta al directorio de trabajo actual del proceso. Si cambias el directorio de trabajo del proceso, el contenido de este enlace simbólico también cambiará para reflejar la nueva ubicación.
- **`/proc/partitions`**: Contiene información sobre las particiones del disco, incluyendo los nombres de los dispositivos y el tamaño de las particiones. Es útil para la administración del almacenamiento y la verificación de las particiones.
- **`/proc/version`**: Muestra información sobre la versión del kernel de Linux en ejecución, incluyendo detalles de la compilación. Es importante para saber exactamente qué versión del kernel está operando.

# **/opt – Software opcional**

Tradicionalmente, el directorio /opt se utiliza para instalar/almacenar los archivos de aplicaciones de terceros que no están disponibles en el repositorio de la distribución.

La práctica normal es mantener el código del software en opt y luego enlazar el archivo binario en el directorio /bin para que todos los usuarios puedan ejecutarlo.

# **/root – El directorio principal de la raíz**

También existe el directorio /root, que funciona como el directorio principal del usuario root. Así que en lugar de /home/root, el hogar de root se encuentra en /root. No lo confunda con el directorio raíz (/).

# **/media – Punto de montaje para medios extraíbles**

Cuando conectas un medio extraíble como un disco USB, una tarjeta SD o un DVD, se crea automáticamente un directorio bajo el directorio /media para ellos. Puede acceder al contenido de los medios extraíbles desde este directorio./media – Punto de montaje para medios extraíbles

# **/mnt – Montar directorio**

Es similar al directorio /media, pero en lugar de montar automáticamente el medio extraíble, mnt es utilizado por los administradores del sistema para montar manualmente un sistema de archivos.

# **/srv – Datos de servicio**

El directorio /srv contiene los datos de los servicios proporcionados por el sistema. Por ejemplo, si ejecuta un servidor HTTP, es una buena práctica almacenar los datos del sitio web en el directorio /srv.

Creo que toda esta información es suficiente para que entiendas la estructura de directorios de Linux y su uso.

Al final, si quieres, puedes descargar y guardar esta imagen para tener una referencia rápida de la estructura de directorios en los sistemas Linux.


# **PATH**
`PATH` es una variable que lista los directorios en los que el sistema operativo buscará para encontrar ejecutables cuando se escriba un comando en la terminal.

- `/usr/local/sbin`: Directorio para programas de administración del sistema para todos los usuarios.
- `/usr/local/bin`: Directorio para programas que no son del sistema, instalados por el administrador del sistema.
- `/usr/sbin`: Directorio para programas de administración del sistema.
- `/usr/bin`: Directorio para programas ejecutables del sistema.
- `/sbin`: Directorio para programas de administración del sistema.
- `/bin`: Directorio para programas esenciales requeridos durante el arranque del sistema o para el uso de herramientas de recuperación.

Cuando se ejecuta un comando en la terminal, el sistema operativo busca en cada uno de estos directorios en el orden en que se especifican en la variable `PATH`. Si encuentra un ejecutable con el nombre especificado, lo ejecuta. Este comando modifica la variable `PATH` para incluir estos directorios específicos en el orden mencionado.

```
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```


![[Pasted image 20231113074648.png]]
