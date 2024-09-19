`socat` (short for "SOcket CAT") es una herramienta que actúa como un "multiplexor de datos de socket bidireccional". Es decir, puede conectar flujos de datos entre diferentes protocolos y puntos de terminación de manera flexible. Se puede considerar como una versión más avanzada de `netcat`, ya que soporta una variedad más amplia de protocolos y configuraciones.

```
https://github.com/3ndG4me/socat
```

# Pasos para hacer pivoting con socat
Configuramos la maquina puente, es decir la maquina intermediaria con socat para que nos proporcione el acceso a la maquina a la cual queremos hacer pivoting
```
socat TCP-L:4444,fork TCP:<host_final>:22
```
- `TCP-LISTEN:4444`: Esto hace que `socat` escuche en el puerto 4444 en Host B.
- `fork`: Permite que `socat` maneje múltiples conexiones entrantes.
- `TCP:HostC:22`: Redirige las conexiones recibidas en el puerto 4444 hacia el puerto 22 (SSH) en Host C.

Ahora con nuestra maquina nos ponemos en escucha
```
nc <host_intermediario> 4444
```
- `HostB`: Es la dirección IP o el nombre de dominio de Host B.
- `4444`: Es el puerto en el que `socat` está escuchando en Host B.

Ahora ya podriamos interactuar con la maquina a la cual no teniamos acceso por el puerto 4444, por ejemplo al haber conectado el puerto 22 podriamos conectanos de la siguiente manera
```
ssh usuario@localhost -p 4444
```

