Arpspoof es una herramienta de hacking informático utilizada para llevar a cabo ataques de suplantación de ARP (Address Resolution Protocol). El ARP es un protocolo utilizado para asociar direcciones IP con direcciones MAC en una red local.

Cuando un dispositivo quiere comunicarse con otro en la misma red local, utiliza ARP para determinar la dirección MAC del destino. Arpspoof aprovecha esta funcionalidad para realizar ataques de suplantación, lo que significa que engaña a otros dispositivos en la red haciéndoles creer que la dirección MAC del dispositivo atacante es la dirección MAC del enrutador o de otro dispositivo legítimo en la red.

Estos ataques pueden ser utilizados para diversos fines maliciosos, como interceptar el tráfico de red, redirigir el tráfico a un destino diferente, realizar ataques de denegación de servicio, o llevar a cabo ataques de intermediario (man-in-the-middle) para interceptar datos confidenciales, como contraseñas o información de inicio de sesión.


### Comandos
- `-i <interfaz>`: Especifica la interfaz de red que se utilizará para llevar a cabo el ataque de suplantación ARP.
- `-t <IP_víctima>`: Especifica la dirección IP de la víctima que se suplantará en el ataque de ARP spoofing.
- `-r <IP_router>`: Especifica la dirección IP del router o de la puerta de enlace cuya identidad se suplantará en el ataque de ARP spoofing.
- `-v`: Modo verbose, que proporciona una salida detallada sobre las actividades realizadas por `arpspoof`.
- `-c`: Modo continuo, que hace que `arpspoof` siga suplantando direcciones ARP indefinidamente en lugar de detenerse después de un período de tiempo predeterminado.
- `-w <archivo>`: Guarda la salida de `arpspoof` en un archivo especificado.


### Ejemplo
arpspoof -i eth1 -t 10.100.13.37 -r 10.100.13.36
![[Pasted image 20240315115154.png]]