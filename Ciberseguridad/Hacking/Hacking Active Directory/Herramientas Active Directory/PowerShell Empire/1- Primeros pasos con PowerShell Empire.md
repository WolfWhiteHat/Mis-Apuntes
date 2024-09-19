PowerShell Empire es un marco de post-explotación de código abierto utilizado para la administración remota de sistemas Windows. Fue diseñado para ayudar a los profesionales de seguridad a realizar pruebas de penetración y evaluar la seguridad de los sistemas. La herramienta se basa en el lenguaje de scripting PowerShell de Microsoft y proporciona una serie de módulos y funcionalidades para la explotación, la persistencia en sistemas comprometidos, el movimiento lateral y la recopilación de información. Sin embargo, es importante destacar que PowerShell Empire también puede ser utilizada con fines maliciosos, por lo que debe ser empleada de manera ética y legal, preferiblemente como parte de un análisis de seguridad autorizado.

# Instalación y uso de PowerShell Empire

Para instalar PowerShell Empire ejecutaremos el siguiente comando
```
sudo apt-get update && sudo apt-get install powershell-empire starkiller -y
```
![[Pasted image 20240422191503.png]]

Una vez instalado ejecutaremos el servidor, para ello ejecutamos el siguiente comando
```
sudo powershell-empire server
```
![[Pasted image 20240422191734.png]]

Ahora en otra pestaña ejecutamos el cliente de PowerShell Empire
```
sudo powershell-empire client
```
![[Pasted image 20240422192000.png]]![[Pasted image 20240422192034.png]]


Continuamos ejecutando el siguiente programa que se conectara al servidor de empire, este programa se llama starkiller, como podemos ver se conecta al puerto que hemos abierto en empire, el usuario es empireadmin y la contraseña  es password123

![[Pasted image 20240422192311.png]]

Una vez dentro configuraremos un oyente
![[Pasted image 20240422194112.png]]

Preparamos ahora el ejecutable para el oyente, esta funcion esta en stage
![[Pasted image 20240422194209.png]]

Una vez preparado lo descargaremos y solo faltara ejecutarlo en la maquina victima
![[Pasted image 20240422194256.png]]

Ahora prepararemos un servidor python para descargar el archivo en la maquina victima
```
sudo python3 -m http.server 80
```
![[Pasted image 20240422194338.png]]


Lo descargamos y ejecutamos en la maquina victima
![[Pasted image 20240422194429.png]]

Si ahora vamos a la pestaña de agentes podemos ver que ya hemos obtenido acceso a la maquina
![[Pasted image 20240422194508.png]]

Si accedemos dentro del agente podremos ejecutar comandos desde nuestra maquina a la maquina victima
![[Pasted image 20240422194738.png]]

A diferencia de metasploit tenemos una opcion muy interesante en la cual podemos listar los directorios de la maquina victima como veremos en la siguiente imagen
![[Pasted image 20240422194826.png]]

Ahora accediendo al terminal donde hemos ejecutado el cliente de empire podremos ver la conexión de la maquina
```
agentes
```
![[Pasted image 20240422195041.png]]
![[Pasted image 20240422195458.png]]
Con el sigueinte comando podremos ver las interacciones que hemos realizado
```
interact [Nombre maquina]
```
![[Pasted image 20240422195205.png]]