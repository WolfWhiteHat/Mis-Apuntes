Este modulo permite desplegar mediante una petición web un _**payload**_ sobre una máquina concreta. En otras palabras, si estamos haciendo uso de un [Bypass de UAC en Windows con Powershell](http://www.elladodelmal.com/2017/02/como-saltarse-el-control-de-cuentas-de.html) y queremos ejecutar un _**Meterpreter**_ a través de _**Powershell**_ podremos hacer una petición a este servicio y obtener un _**shell Meterpreter**_ en formato _**PSHell**_. También será posible obtener un _**payload**_ para ser ejecutado en [Python](http://0xword.com/es/libros/66-libro-python-pentesters.html) y en _**PHP**_, por lo que hace fundamental conocer este módulo y su uso.

`exploit/multi/script/web_delivery
# Configuración exploit
Primero configuramos el exploit
![[Pasted image 20240528135256.png]]
![[Pasted image 20240528134157.png]]

El target lo seleccionamos dependiendo de donde queramos ejecutar la carga
![[Pasted image 20240528135314.png]]

Una vez configurado el exploit lo ejecutamos
![[Pasted image 20240528134357.png]]

Copiamos el codigo de abajo y lo ejecutaremos en la terminal que tenemos abierta de windows
![[Pasted image 20240528134848.png]]

Una vez ejecutado como podemos ver obtenemos una sesion de meterpreter
![[Pasted image 20240528134523.png]]

Aqui tenemos la sesion de meterpreter con los privilegios mas altos
![[Pasted image 20240528134612.png]]

Realizado en maquina blaster
https://tryhackme.com/r/room/blaster

https://www.reydes.com/d/?q=Explotar_un_Sistema_Windows_utilizando_el_modulo_web_delivery_de_MSF

