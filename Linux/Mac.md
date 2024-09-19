Los primeros 3 bytes (24 bits) representan el fabricante de la tarjeta, y los últimos 3 bytes (24 bits) identifican la tarjeta particular de ese fabricante. Cada grupo de 3 bytes se puede representar con 6 **dígitos** hexadecimales, formando un número hexadecimal de 12 **dígitos** que representa la **MAC** completa.

Para saber la mac escribimos ifconfig y revisamos el apartado ether
![[Pasted image 20240214085733.png]]
ether e6:38:05: e3:93:74
ether 06:20:7:1:1:db

Como podemos ver estas son las dos mac que tiene mi maquina virtual en cada interfaz, para cambiar la mac utilizaremos el siguiente comando
macchanger -m 00:A2:E4:56:78:C0 eth0
![[Pasted image 20240214085956.png]]

Accediendo desde root como podemos ver ya me ha cambiado la mac