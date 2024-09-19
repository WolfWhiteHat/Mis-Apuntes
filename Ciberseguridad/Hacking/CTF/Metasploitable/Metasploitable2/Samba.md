Samba es un software de código abierto que permite a los sistemas operativos basados en Unix compartir archivos, impresoras y otros recursos con sistemas Windows. Es compatible con una amplia gama de sistemas operativos, incluidos Linux, macOS y Solaris.

Para empezar a explotar la vulnerabilidad de samba primero deberemos saber que versión tiene exactamente porque como podemos ver en el escaner de nmap no se puede ver la versión completa
![[Pasted image 20240130101500.png]]

Para ello ejecutaremos el siguiente auxiliar en metasploit
![[Pasted image 20240130101651.png]]
Después de ejecutarlo ya sabremos la versión exacta de samba

Ahora prepararemos el exploit para realizar el ataque
![[Pasted image 20240130102626.png]]

Configuramos la ip de la maquina atacante y la victima
![[Pasted image 20240130103153.png]]

Una vez tenemos preparado el ataque solo tenemos que lanzarlo
![[Pasted image 20240130103755.png]]