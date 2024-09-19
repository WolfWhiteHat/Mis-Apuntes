**BloodHound** es una herramienta de análisis de ataque y visualización para Active Directory que utiliza Neo4j como base de datos para almacenar y consultar datos.

**Neo4j** es una base de datos de grafos, diseñada específicamente para almacenar y procesar datos relacionales en forma de grafos.

# **Bloodhount**
```
https://github.com/BloodHoundAD/BloodHound
```

# **Bloodhount Pyhton**
```
https://github.com/fox-it/BloodHound.py
```

# Instalación BloodHound y Neo4j
Para instalar BloodHound y Neo4j ejecutaremos el siguiente comando
```
sudo apt install bloodhound neo4j
```
![[Pasted image 20240718080438.png]]

# Iniciar consola neo4j
```
sudo neo4j console
```
![[Pasted image 20240718081931.png]]

Como vemos en la imagen se nos genera un enlace para acceder al portal, tanto el user como la passwd por defecto es `neo4j`, en el primer inicio de sesión nos solicitara cambiar la password
```
http://localhost:7474/
```
![[Pasted image 20240718082037.png]]

Una vez cambiamos la password nos enviara al portal de neo4j
![[Pasted image 20240718082323.png]]

Ahora ejecutaremos `bloodhount`con el siguiente comando
```
bloodhound
```

Al ejectuarlo se nos abrira una terminal en la cual nos loguearemos con el mismo usuario de neo4j
![[Pasted image 20240718082625.png]]

Una vez logueados ya estemos en el menu principal de bloodhount
![[Pasted image 20240718083634.png]]

Ahora necesitaremos instalar BloodHound.py para poder obtener la informacion del dominon, para ello podemos hacerlo de dos formas, instalandolo con pip o desde el repostiorio de github
```
pip3 install bloodhound
```
![[Pasted image 20240718084225.png]]

Y ejecutando el siguiente comando obtenemos toda la información de la maquina victima
```
bloodhound-python -u svc-admin -p management2005 -ns 10.10.193.144 -d spookysec.local -c all
```
![[Pasted image 20240718092111.png]]
- `-u`: Especifica el usuario
- `-p`: Especifica la contraseña
- `-ns 10.10.193.144`: Indica la dirección IP (`10.10.193.144`) del servidor DNS que se utilizará para resolver nombres en el dominio (`spookysec.local`)
- `-d spookysec.local`: Especifica el nombre del dominio de Active Directory
- `-c all`: Indica que se deben recoger todos los datos posibles durante la exploración

Ahora solo falta cargar los archivos en `bloodhound` y ya nos mostrara toda la información, para cargar la información tenemos este boton
![[Pasted image 20240718092255.png]]

Y seleccionamos los ficheros previamente obtenidos
![[Pasted image 20240718092328.png]]

Aquí podremos ver los avances de la subida
![[Pasted image 20240718092402.png]]

Ahora con toda la información subida si accedemos al menu de arriba a la izquierda y seleccionamos el usuario comprometido podremos revisar toda la información
![[Pasted image 20240718093035.png]]

Seleccionamos al usuario como owned
![[Pasted image 20240718093105.png]]

Y ahora si vamos a analizar podremos revisar todas sus vulnerabilidades y a que tenemos acceso con este usuario y como escalar privilegios
![[Pasted image 20240718093219.png]]

Realizado en la maquina [[MAQUINA ATTACKTIVE DIRECTORY(enum4linux, kerbrute enumerar usuarios, ASREPRoasting obtener TGT, john the ripper, smbclient para listar recursos compartidos, secredump dumpear hashes y pass the hash)]]


-----
# **Resolver problema resolución DNS**
Si al ejecutar el comando para la obtención de los datos con bloodhound obtenemos una respuesta la cual nos da error en la resolucion de DNS realizaremos los siguientes configuraciones, primero añadiremos en nuestro `/etc/hosts` el nombre
![[Pasted image 20240718091505.png]]

Añadiremos en el archivo `/etc/resolv.conf` la ip de la maquina
![[Pasted image 20240718091607.png]]

Y ahora podemos usar nslookup y dig para verificar si ya esta resuelto el problema de la resolucion de DNS
```
nslookup -type=SRV _ldap._tcp.spookysec.local 10.10.193.144
```
![[Pasted image 20240718091654.png]]

Y con dig
```
dig @10.10.193.144 _ldap._tcp.spookysec.local SRV
```
![[Pasted image 20240718091737.png]]
- `_ldap`: Es el nombre del servicio que estamos buscando. En este caso, `_ldap` se refiere a Lightweight Directory Access Protocol, utilizado comúnmente en sistemas de directorios como Active Directory de Microsoft.
- `_tcp`: Indica el protocolo utilizado, en este caso, TCP (Transmission Control Protocol).
- `spookysec.local`: Es el nombre del dominio donde se está buscando el registro SRV.