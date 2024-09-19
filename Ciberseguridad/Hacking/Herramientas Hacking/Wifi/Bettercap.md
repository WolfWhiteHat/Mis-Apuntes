Bettercap es una herramienta de código abierto para pruebas de penetración y análisis de redes. Está diseñada para ser fácil de usar y entender, incluso para aquellos que no tienen mucha experiencia en seguridad informática. Bettercap puede utilizarse para realizar una variedad de tareas, incluyendo:

- Escaneo de redes
- Detección de vulnerabilidades
- Ataques de denegación de servicio (DoS)
- Ataques de hombre en el medio (MitM)
- Recopilación de información
- Y mucho más

https://www.bettercap.org/

# Auditar red wifi
Primero conectamos la tarjeta de red y lo comprobamos
ifconfig
La tarjeta deberia aparecer como WLAN

## **Poner la tarjeta en modo monitor**
```Bash
sudo airmon-ng start wlan0
```
Para revisar los handshakes tendremos que ir a la carpeta root que es donde se almacenan por defecto.

# Arrancar la herramienta
```Bash
sudo bettercap -iface wlan0mon
```

Una vez dentro activaremos el modulo wifi
```Bash
wifi.recon on
```

Mostrar todas las wifis que ha captado 
```Bash
wifi show
```

Con el comando help veremos todos los modulos disponibles, para arrancarlos o pararlos utilizar on/off después del modulo