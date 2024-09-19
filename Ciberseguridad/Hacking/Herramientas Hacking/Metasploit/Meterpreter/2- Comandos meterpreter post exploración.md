sysinfo
![[Pasted image 20240327114906.png]]

getuid
![[Pasted image 20240327114922.png]]


checksum md5 /bin/bash
![[Pasted image 20240327115319.png]]
Para calcular el checksum MD5 del archivo "/bin/bash", se puede usar el comando "md5sum" en sistemas UNIX como Linux. El checksum MD5 es una secuencia alfanumérica de 32 caracteres que representa la suma de verificación (hash) de un archivo. Aquí está el comando para calcular el checksum MD5 de "/bin/bash":


getenv PATH
![[Pasted image 20240327115338.png]]
El comando "getenv PATH" en Meterpreter se utiliza para obtener información sobre la variable de entorno PATH en el sistema objetivo. La variable PATH es una variable de entorno en sistemas operativos tipo UNIX (como Linux) que especifica las ubicaciones de directorios en las que el sistema busca ejecutables cuando se ingresa un comando en la línea de comandos.

El resultado que has compartido indica las rutas especificadas en la variable PATH en el sistema objetivo:

- `/usr/local/sbin`
- `/usr/local/bin`
- `/usr/sbin`
- `/usr/bin`
- `/sbin`
- `/bin`

Estas rutas especifican los directorios donde se pueden encontrar ejecutables en el sistema. Cuando se ingresa un comando en la línea de comandos, el sistema buscará en estos directorios para encontrar el ejecutable correspondiente.



search -f *php*
![[Pasted image 20240327115225.png]]

execute -f ifconfig
![[Pasted image 20240327114957.png]]


## Abrir sesion shell Linux
shell
/bin/bash -i

## Abrir sesion shell Windows
shell