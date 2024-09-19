Wifipumpkin3 es una herramienta de hacking ético y pentesting diseñada para realizar pruebas de seguridad en redes inalámbricas. Permite realizar ataques como "man-in-the-middle" y capturar contraseñas de redes Wi-Fi, entre otras funcionalidades. Wifipumpkin3 es una herramienta avanzada que puede ser utilizada por profesionales de la seguridad informática para evaluar la seguridad de redes inalámbricas y detectar posibles vulnerabilidades.

### Comandos
- iw liss: Muestra todos los modos que puedes configurar en la tarjeta inalambrica

### Arrancar herramienta por primera vez
sudo wifipumkin3

La primera vez que arrancamos esta herramienta tarda un poco mas al iniciarse porque crea los direcctorios donde se almacena la información la ruta es la siguiente:
root/.config/wifipumkin3


### Configuración y preparación de entorno
Volvemos a arrancar la herramienta
sudo wifipumkin3

Una vez dentro de la herramienta le damos a help para obtener todos los comandos y su información

Es una aplicación similar a metasploit

Seleccionamos ap y nos aparecera la configuración para ejecutarlo

#### Seleccionar interfaz
set interface wlan0
set ssid Test

Ahora le diremos que ignore todos los registros DNS
ignore pydns_serevr

#### Portales cautivos
Continuamos seleccionando los modulos
para ver los modulos podemos revisarlos con el comando:
show

para seleccionarlo utilizaremos el siguiente comando:
use misc.extra.captiveflask

una vez dentro del modulo listaremos los comandos:
help

Ahora descargargaremos los portales cautivos
download
list

continuaremos instalado los portales cautivos que queramos, podemos instalar los nuestros propios, seleccionamos el que queremos
install microsoft

Listamos que este instalado el portal
list

Volvemos hacia atras con el comando:
back

#### Configuración proxy
Inciamos la configuración escribiendo:
proxies

para activar el proxy:
set proxy captiveflask

para ver si ha activado el proxy que queremos listamos con el comando:
proxies

#### Configurar redirección
set captiveflashk.force_redirect_to_url https://google.com

#### Captive Portal Plugins
set captiveflask.facebook
proxies

#### Ejecutar la herramienta
start 
Es posible que la primera vez que ejecutemos la herramienta pueda fallar, simplemente volveremos a ejecutar la herramienta y la volveremos a lanzar, no es necesario volver a configurar todos los parametros porque ya están almacenados aun que no esta de mas revisarlos para garantizar que este bien configurado
