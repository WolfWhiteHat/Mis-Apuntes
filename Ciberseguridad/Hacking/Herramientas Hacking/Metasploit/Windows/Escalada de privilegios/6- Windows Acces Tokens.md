Los "tokens de acceso" (access tokens) en Windows son una parte fundamental del sistema de seguridad de Windows. Estos tokens son utilizados para representar la identidad y los privilegios de un usuario o un proceso en particular en el sistema operativo Windows. Cuando un usuario se autentica en Windows, se le asigna un token de acceso que contiene información sobre su identidad (como su nombre de usuario) y los privilegios que tiene en el sistema (como los grupos a los que pertenece y los permisos que tiene).

Los tokens de acceso se utilizan para controlar el acceso a recursos del sistema, como archivos, carpetas, impresoras y otros objetos de sistema. Cuando un usuario intenta acceder a un recurso, el sistema operativo verifica si el usuario tiene los permisos necesarios para realizar la acción solicitada examinando su token de acceso.

Los tokens de acceso también se utilizan para la comunicación entre procesos en Windows. Cuando un proceso inicia otro proceso en nombre de un usuario, el nuevo proceso hereda el token de acceso del proceso principal. Esto asegura que el nuevo proceso tenga los mismos privilegios que el proceso principal y que pueda acceder a los mismos recursos.

En resumen, los tokens de acceso en Windows son una parte fundamental del sistema de seguridad que se utiliza para representar la identidad y los privilegios de los usuarios y procesos, y controlar el acceso a recursos del sistema.

lsas.exe es el servicio del subsistema de autoridad de seguridad


### Practica 

Primero realizamos un escaneo con nmap
![[Pasted image 20240311124936.png]]

Una vez escaneado los puertos revisaremos las posibiles vulnerabilidades que tiene desde searchsploit
![[Pasted image 20240311125211.png]]

Ahora que ya hemos ejecutado metasploit utilizaremos el siguiente modulo para obtener acceso
exploit/windows/http/rejetto_hfs_exec
![[Pasted image 20240311130141.png]]

Como veremos en la siguiente imagen no tenemos permisos para poder leer un fichero, para ello realizaremos una escalada de privilegios para poder tener acceso a los documentos
![[Pasted image 20240311130337.png]]

Cargamos el modo incognito y revisamos los tokens
load incognito
list_tokens -u
![[Pasted image 20240311130538.png]]

Como vemos estos son los tokens de los cuales poden disponer, ahora suplantaremos el token de administrador
impersonate_token ATTACKDEFENSE\\Administrator
getuid
![[Pasted image 20240311131017.png]]

En la ultima imagen vemos como hemos aumentado nuestro privilegios, si ahora intentamos utilizar el comando anterior veremos que ahora si tenemos permisos
![[Pasted image 20240311131212.png]]