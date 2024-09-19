

Vamos a realizar un envenenamiento ARP

Para ello primero analizaremos el trafico
nmap 10.100.13.140/24
![[Pasted image 20240315114918.png]]


echo 1 > /proc/sys/net/ipv4/ip_forward
![[Pasted image 20240315115018.png]]
- `echo 1`: Esta parte del comando `echo` simplemente envía el valor `1` como salida. En Linux, el comando `echo` se utiliza para imprimir texto o valores en la salida estándar.
- `>`: El operador de redirección `>` se utiliza para redirigir la salida del comando `echo` hacia un archivo o una ubicación específica. En este caso, no se redirige hacia un archivo, sino hacia `/proc/sys/net/ipv4/ip_forward`.
- `/proc/sys/net/ipv4/ip_forward`: Este es un archivo especial en el sistema de archivos `/proc` de Linux que controla el reenvío de paquetes IP en el kernel del sistema operativo. Al escribir `1` en este archivo, se activa el reenvío de paquetes IP, lo que permite que el sistema reenvíe los paquetes entre diferentes interfaces de red.

En resumen, este comando activa el reenvío de paquetes IP en el kernel del sistema operativo Linux, lo que permite que el sistema actúe como un enrutador al reenviar paquetes entre diferentes interfaces de red. Es útil en situaciones donde se desea utilizar un sistema Linux como un enrutador o un dispositivo de red.


arpspoof -i eth1 -t 10.100.13.37 -r 10.100.13.36
![[Pasted image 20240315115154.png]]


Ejecutamos wirewhark y revisamos del trafico que hay el que hemos generado con el anterior comando

![[Pasted image 20240315115431.png]]
![[Pasted image 20240315115446.png]]
![[Pasted image 20240315115526.png]]

telnet 10.100.13.36
![[Pasted image 20240315115713.png]]
![[Pasted image 20240315115734.png]]