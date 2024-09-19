
Primero realizamos un escaneo del servicio a explotar
```
nmap -sV -sC -p445 10.2.25.55
```
![[Pasted image 20240502074850.png]]

Revisamos si hay alguna vulnerabilidad de la versión del servicio y vemos que metasploit tiene un modulo para explotar
![[Pasted image 20240502075020.png]]

Buscamos y seleccionamos el modulo
![[Pasted image 20240502075108.png]]

Lo configuramos
![[Pasted image 20240502075132.png]]

Y lo ejecutamos, como podemos ver obtenemos una sesión en la maquina victima
![[Pasted image 20240502075237.png]]

Revisamos algunas carpetas para obtener información
`cat /etc/*issue`
![[Pasted image 20240502075343.png]]

`cat /etc/*release`
![[Pasted image 20240502075438.png]]

