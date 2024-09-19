ifconfig
![[Pasted image 20240219185534.png]]

Como podremos ver en la siguiente imagen la tarjeta de red esta en modo managed y queremos ponerla en modo monitor
iwconfig
![[Pasted image 20240219185553.png]]

lsusb -vv
![[Pasted image 20240219185712.png]]


### Activar modo monitor
airmon-ng start wlan0
![[Pasted image 20240219190330.png]]

Matar procesos
airmon-ng check kill
![[Pasted image 20240219191006.png]]


Como podemos ver ya tenemos la tarjeta de red en modo monitor
![[Pasted image 20240219191118.png]]