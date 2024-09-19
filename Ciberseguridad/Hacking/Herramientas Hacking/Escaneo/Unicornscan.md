Unicornscan es una herramienta diseñada para descubrir dispositivos en red y detección de puertos, es similar a Nmap

unicornscan -mT [ip/rango de red]
unicornscan -mT 192.168.1.1:1-100


- m: modo de escaneo, especificamos el protocolo, mT (TCP), mU (UDP), mI(ICMP)
- I: interfaz de red, ejemplo -I eth0, especificas que interfaz quieres que haga el escaneo
- p: especificar que puertos deseas escanear
- r: especifica numero de hilos
- L: guarda los resultados en un archivo
- b: define la fuerza de conexión, especifica la velocidad de conexión

unicornscan --help
unicornscan comando --help
