Netdiscover es una herramienta para descubrir hosts en una red, trabaja con el protocolo ARP, es decir es decir escanea la red realizando peticiones ARP.


Primero instalamos la herramienta

apt-get install netdiscover
![[Pasted image 20240228114606.png|1000]]

netdiscover -i eth1 -r 192.168.60.0/24
![[Pasted image 20240228115137.png]]
![[Pasted image 20240228115151.png]]