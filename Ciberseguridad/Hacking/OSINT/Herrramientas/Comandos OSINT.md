# Nslookup
`nslookup` es una herramienta de línea de comandos utilizada para consultar y resolver información de DNS (Sistema de Nombres de Dominio). Con `nslookup`, puedes obtener información sobre nombres de dominio, direcciones IP, registros de recursos y otros detalles relacionados con la resolución de nombres.

https://axarnet.es/blog/que-es-nslookup#


# Dig
Dig (Domain Information Groper) es una herramienta de línea de comandos de Linux que realiza búsquedas en los registros DNS, a través de los nombres de servidores, y te muestra el resultado.
De forma predeterminada, dig envía la consulta DNS a todos los nombres de servidores listados en el archivo resolver (/etc/resolv.conf), a menos de que se le pida que realice la consulta con un nombre de servidor específico.

dig hackersploit.org
![[Pasted image 20240313104530.png]]

## Respuesta corta
dig hackersploit.org +short
![[Pasted image 20240313104548.png]]

## Respuesta detallada
dig hackersploit.org +noall +answer
![[Pasted image 20240313104612.png]]

## Especificar servidores de nombres
dig @8.8.8.8 hackersploit.org
![[Pasted image 20240313104641.png]]

## Consultar todos los registros DNS
dig hackersploit.org any
![[Pasted image 20240313104702.png]]

## Buscar por tipo de registro
dig hackersploit.org MX
![[Pasted image 20240313104721.png]]

## Trazar ruta
dig hackersploit.org +trace
![[Pasted image 20240313104748.png]]
## Busqueda inversa de DNS
dig +answer -x [IP]
![[Pasted image 20240313104831.png]]

## Ejemplo completo
dig +nocmd testbhpro.zone MX +noall +answer
![[Pasted image 20240313104937.png]]

## Ataque transferencia de zona
dig axfr @nsztm1.digi.ninja zonetransfer.me
![[Pasted image 20240313105027.png]]

dig ixfr @nsztm1.digi.ninja zonetransfer.me
También podriamos realizar el ataque con ixfr de forma incremental


# Dnsrecon
DNSRecon es una herramienta de código abierto utilizada para realizar el análisis de infraestructura de DNS y la enumeración de registros DNS. Esta herramienta está diseñada para ayudar en la recopilación de información sobre un dominio específico, incluyendo subdominios, registros MX (Mail Exchange), servidores de nombres (NS), direcciones IP y otros tipos de registros DNS.

Algunas de las características de DNSRecon incluyen la capacidad de realizar búsquedas de subdominios, enumerar registros DNS, realizar transferencias de zona, buscar registros de servicios (SRV), y realizar resolución inversa de direcciones IP.

DNSRecon es útil para investigadores de seguridad, administradores de sistemas y profesionales de ciberseguridad para obtener una visión más completa de la infraestructura de DNS de un dominio y detectar posibles vulnerabilidades o puntos débiles en la configuración DNS.

https://github.com/darkoperator/dnsrecon

## Instalar DNSrecon
wget https://github.com/darkoperator/dnsrecon
![[Pasted image 20240313101130.png]]

dnsrecon -h hackersploit.org
![[Pasted image 20240313101228.png]]

# Fierce
Fierce es una herramienta de enumeración de subdominios que utiliza la transferencia de zona (zonetransfer) y la búsqueda de registros DNS (bruteforce) para recopilar información sobre los subdominios asociados con un dominio específico. Es una herramienta de código abierto que se utiliza comúnmente en pruebas de penetración y en la recopilación de información durante las fases de reconocimiento de un test de penetración.

Fuerza bruta con fierce
fierce --domain zonetransfer.me
![[Pasted image 20240313103134.png]]


# Host
El comando `host` es una herramienta de línea de comandos utilizada en sistemas basados en Unix y Linux para realizar consultas DNS y obtener información sobre nombres de dominio y direcciones IP. Permite realizar consultas de resolución de nombres, inversa y de búsqueda de registros DNS.

Aquí hay una descripción general de cómo utilizar el comando `host`:

1. **Resolución de Nombres de Dominio**:
    - Para resolver un nombre de dominio en una dirección IP, simplemente escribe `host` seguido del nombre de dominio.
    - Ejemplo: `host example.com`
2. **Resolución Inversa**:
    - Para obtener el nombre de dominio asociado con una dirección IP, puedes utilizar el comando `host` seguido de la dirección IP.
    - Ejemplo: `host 192.0.2.1`
3. **Búsqueda de Registros DNS Específicos**:
    - Puedes buscar registros DNS específicos utilizando la opción `-t` seguida del tipo de registro que deseas buscar. Algunos tipos comunes incluyen A (registro de dirección IP), MX (registro de intercambio de correo), NS (registro de servidor de nombres), entre otros.
    - Ejemplo: `host -t MX example.com`
4. **Control de la Consulta**:
    - Puedes especificar un servidor DNS específico para realizar la consulta utilizando la opción `-T`. Esto es útil para consultar servidores DNS específicos en lugar de usar el servidor DNS predeterminado del sistema.
    - Ejemplo: `host -T 8.8.8.8 example.com`


host hackersploit.org
![[Pasted image 20240313105553.png]]


# Htttrack
HTTrack es una herramienta de código abierto que se utiliza para descargar sitios web completos de Internet para su posterior visualización sin conexión. Funciona creando una copia exacta de un sitio web, incluyendo todos sus archivos HTML, imágenes, hojas de estilo CSS, scripts JavaScript y otros recursos vinculados. Esta copia descargada se almacena localmente en el disco duro del usuario y puede ser navegada como si estuviera accediendo al sitio web en línea.

HTTrack es útil para una variedad de propósitos, como acceder a sitios web sin conexión a Internet, realizar copias de seguridad de sitios web completos, realizar pruebas de desarrollo web en entornos locales, o simplemente para acceder a sitios web que podrían estar temporalmente inaccesibles o con una conexión de Internet intermitente.

https://www.httrack.com/
Herramienta para la descarga de paginas web y revisión del código fuente



# Whois
whois hackersploit.org
![[Pasted image 20240313130609.png]]

whois [IP]
![[Pasted image 20240313130647.png]]