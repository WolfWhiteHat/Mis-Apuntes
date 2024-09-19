Tshark es una herramienta de línea de comandos que se utiliza para capturar y analizar el tráfico de red. Es parte del conjunto de herramientas proporcionado por Wireshark, pero a diferencia de Wireshark, que proporciona una interfaz gráfica de usuario (GUI), Tshark se ejecuta en la línea de comandos, lo que lo hace útil en entornos donde no se puede utilizar una interfaz gráfica.

### Ventajas y mejores usos:

- Tshark es ligero y puede ser utilizado en entornos donde los recursos son limitados o donde no se dispone de una interfaz gráfica de usuario.
- Es altamente personalizable y puede ser integrado en scripts y procesos automatizados para analizar el tráfico de red en tiempo real o para procesar archivos de captura previamente grabados.
- Puede ser utilizado en sistemas remotos a través de SSH, lo que lo hace útil para la administración y análisis de redes en servidores remotos.

### Comandos
- `tshark -r archivo.pcap`: Lee el archivo de captura especificado en lugar de capturar tráfico en vivo.
- `tshark -i interfaz`: Especifica la interfaz de red desde la cual capturar el tráfico.
- `tshark -f filtro`: Aplica un filtro de captura al tráfico para capturar solo los paquetes que coincidan con el filtro especificado.
- `tshark -w archivo.pcap`: Escribe el tráfico capturado en un archivo pcap.
- `tshark -T fields -e campo`: Especifica el formato de salida y el campo que se debe mostrar. Por ejemplo, `-T fields -e ip.src` imprimirá solo las direcciones IP de origen de los paquetes capturados.
- `tshark -Y expresion`: Permite utilizar una expresión de visualización para filtrar los paquetes que se muestran en tiempo real.
- `tshark -z estadísticas`: Muestra estadísticas sobre el tráfico capturado, como resumen de protocolos, estadísticas de flujo, etc.
- `tshark -d`: Muestra las interfaces disponibles en el sistema.
- `tshark -h`: Muestra la lista de opciones de ayuda y comandos disponibles.
- `tshark -v`: Muestra la versión de Tshark instalada.
- `tshark -e`: Permite especificar un campo de la trama que se debe imprimir en la salida.
- - `-Y "http contains password"`: Esta opción especifica un filtro de visualización que se aplicará al archivo de captura. En este caso, el filtro selecciona los paquetes que contienen la cadena "password" en el contenido de la carga útil de cualquier solicitud o respuesta HTTP. Esto significa que el comando buscará cualquier instancia de la palabra "password" en los datos de las comunicaciones HTTP capturadas en el archivo.
- `frame.time`: El tiempo en el que se capturó el paquete.
-  `ip.src`: La dirección IP de origen del paquete.
- `ip.dst`: La direccion IP de destino del paquete
- `http.request.full_uri`: La URL completa de la solicitud HTTP.


### Ejemplos

Todos los ejemplos que vamos a seguir son de la misma practica y con el archivo .pcap
![[Pasted image 20240315110946.png]]

#### Analizar trafico HTTP
tshark -Y 'http' -r HTTP_traffic.pcap
![[Pasted image 20240315111214.png]]
![[Pasted image 20240315111154.png]]

#### Analizar trafico HTTP de una maquina a otra
tshark -r HTTP_traffic.pcap -Y "ip.src==192.168.252.128 && ip.dst==52.32.74.91"
![[Pasted image 20240315111509.png]]

#### Analizar trafico metodo GET
tshark -r HTTP_traffic.pcap -Y "http.request.method==GET
![[Pasted image 20240315111905.png]]
![[Pasted image 20240315111852.png]]


#### Analizar trafico 
tshark -r HTTP_traffic.pcap -Y "http.request.method==GET" -Tfields -e frame.time -e
ip.src -e http.request.full_uri
- `-Tfields`: Esta opción indica a Tshark que el formato de salida debe ser en campos (fields). Esto significa que solo se mostrarán los campos específicos de cada paquete que cumplan con los criterios de filtro especificados anteriormente.
    
- `-e frame.time -e ip.src -e http.request.full_uri`: Estas opciones especifican los campos específicos que se mostrarán en la salida. En este caso, se mostrarán tres campos:
    
    - `frame.time`: El tiempo en el que se capturó el paquete.
    - `ip.src`: La dirección IP de origen del paquete.
    - `http.request.full_uri`: La URL completa de la solicitud HTTP.

![[Pasted image 20240315112117.png]]
![[Pasted image 20240315112059.png]]


#### Analizar trafico palabras
tshark -r HTTP_traffic.pcap -Y "http contains password"
![[Pasted image 20240315112350.png]]

#### Analizar trafico dirigido a pagina web
tshark -r HTTP_traffic.pcap -Y "http.request.method==GET && http.host==www.nytimes.com" -Tfields -e ip.dst
![[Pasted image 20240315112753.png]]


#### Analizar trafico mostrando ip de destino y las cookies
tshark -r HTTP_traffic.pcap -Y "ip contains amazon.in && ip.src==192.168.252.128" -Tfields -e ip.src -e http.cookie
![[Pasted image 20240315112946.png]]
![[Pasted image 20240315112931.png]]

#### Analizar trafico SO
tshark -r HTTP_traffic.pcap -Y "ip.src==192.168.252.128 && http" -Tfields -e http.user_agent
![[Pasted image 20240315113205.png]]


### Wifi con Tshark

tshark -r Wifi_traffic.pcap -Y "wlan"
![[Pasted image 20240315122556.png]]
![[Pasted image 20240315122537.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==0x000c"
![[Pasted image 20240315122650.png]]

tshark -r WiFi_traffic.pcap -Y "eapol"
![[Pasted image 20240315122817.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==8" -Tfields -e wlan.ssid -e wlan.bssid
![[Pasted image 20240315122941.png]]
![[Pasted image 20240315123000.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ssid==LazyArtists" -Tfields -e wlan.bssid
![[Pasted image 20240315123102.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ssid==Home_Network" -Tfields -e wlan_radio.channel
![[Pasted image 20240315123302.png]]
![[Pasted image 20240315123327.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==0x000c" -Tfields -e wlan.ra
![[Pasted image 20240315123425.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ta== 5c:51:88:31:a0:3b && http" -Tfields -e http.user_agent
![[Pasted image 20240315124130.png]]