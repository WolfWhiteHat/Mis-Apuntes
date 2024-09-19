
Ahora vamos a explotar la vulnerabilidad eternal blue

Para ello escanearemos si esta vulnerabilidad esta en la maquina victima
![[Pasted image 20240308085511.png]]
![[Pasted image 20240308085546.png]]

Primero nos descargaremos la herramienta a utilizar de github
https://github.com/3ndG4me/AutoBlue-MS17-010

Seguidamente accederemos a la carpeta del codigo descargado
![[Pasted image 20240308085705.png]]

Ahora le daremos permisos a nuestro usuario en el archivo shellcode
![[Pasted image 20240308085939.png]]

Ejecutaremos shhell_prep.sh y generaremos la reverse shelll con nuestra ip y el puerto que hayamos seleccionado
![[Pasted image 20240308090116.png]]

Ahora con la herramienta de netcat activaremos la escucha por el puerto 1234 que es el que hemos configurado en nuestra reversheel
nc -nvlp 1234
![[Pasted image 20240308090638.png]]


Ejecutaremos el exploit
![[Pasted image 20240308090300.png]]

Una vez ejecutado si volvemos a la pestaña donde teniamos iniciado netcar podremos ver que hemos obtenido la shell
![[Pasted image 20240308090741.png]]

----------------


Esto mismo que acabamos de realizar podriamos ejecutarlo con un modulo de metaslploit, seleccionamos el siguiente modulo
use exploit/windows/smb/ms17_010_eternalblue
![[Pasted image 20240308090826.png]]

Configuramos los parametros y ejecutamos el exploit
![[Pasted image 20240308090951.png]]

![[Pasted image 20240308091103.png]]
![[Pasted image 20240308091129.png]]
![Pasted image 20240308091129.png](app://36ea27c7ef7ae19504147261a7a262391bf2/Users/ericmoliner/Library/Mobile%20Documents/iCloud~md~obsidian/Documents/Mi%20carpeta/Mis%20apuntes/Ciberseguridad/Vulenrability/Windows/SMB/ANEXOS/Pasted%20image%2020240308091129.png?1709885489178)
![[Pasted image 20240308091212.png]]

Como podemos ver ya hemos obtenido acceso a la maquina con meterpreter desde el exploit de metasploit