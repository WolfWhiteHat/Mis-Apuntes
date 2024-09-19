Nmap es un programa que sirve para el escaneo de equipos en una red, también puede analizar que puertos están abiertos, que servicios se están ejecutando y que vulnerabilidades tiene el sistema
nmap -sV 192.168.1.13
![[Pasted image 20240313143730.png]]


# Comandos Nmap

- `sU`: Escaneo UDP
- `sT`: Escaneo TCP
- `sS`: Escaneo SYN
- `PS`: Escaneo TCP SYN
- `PA`: Escaneo TCP ACK
- `PE`: Escaneo ICMP
- `Pn`: Elimina el descubrimiento de hosts
- `p`: Escaneo de puertos especificos, -p- para todos los puertos
- `F`: Escaneo de los 100 puertos TCP mas comunes
- `sV`: Conocer los servicios detras de los puertos
- `sC`: Scripts de analisis
- `sCV`: Ejecuta los parametro sC y sV
- `sN`: Escaneo ACK, se utiliza para identificar si hay un firewall de por medio
- `sn`: escaneo de host con paquetes ping ICMP
- `vvv`: Verbosidad detallada, cuantas mas v mas detallado sera el resultado
- `n`: Desactivar resolucions DNS
- `oN`: Guarda el resultado en un archivo TXT
- `oX`: Guarda el resultado en un archivo XML
- `oG`: Guarda el resultado en un archivo en formato (greppable output). Significa que se guarda en un formato estructurado para revisar con herramientas como grep, awk, sed.
- `iL`: Escaneo desde un archivo con listas objetivos
- `f`: Fragmenta los paquetes
- `D`: Especifica una ip señuelo para ocultar tu ip real
- `O`: Escaneo de sistema operativo
- `A`: Utiliza las funciones de -sV, -O, --script, --traceroute (Modo agresivo)
- `T2`: Establece nivel de agresividad, T0 o T1 hacen el escaneo mas sigiloso pero mas lento y el mas agresivo es T5
- target/24: Escaneo red completa
- `--open`: Solo analiza puertos abiertos, ni filtrados ni cerrados
- `--send-ip`: Suprimer el DNS y envia los paquetes directamente a las ip
- `--osscan-gues`: Similar al comando O, pero es menos preciso, mas rápido y menos intrusivo
- `--version-intensity`: Especifica la agresividad del escaneo de versiones, va des de el 0-9 de menor a mayor agresividad
- `--mtu`: Especifica el tamaño minimo de la unidad de transmision
- `--host-timeout`: Especifica el tiempo máximo que espera la respuesta de un host
- `--scan-delay`: Establece un retraso entre los escaneos de puertos consecutivos, previene la deteccion de sistemas IPS o IDS
- `--script`: Selecciona un script a escanear
- `--script-discovery`: Activa una serie de scripts diseñados para descubrir y recolectar información básica sobre la red y los sistemas objetivo
- `--script-args`: Se utiliza para añadir argumentos adicionales a los scripts

# Comandos atajos
- `A`: Utiliza las funciones de O, --version-intensity 9 y --script=default

Con la tecla espacio sabremos el porcentaje del escaneo

----------

# Tipos de escaneo con Nmap

## Escaneo ip publica
Si la respuesta está abierta para los puertos 21, 22, 25, 80, 443 o 3389, lo más probable es que el reenvío de puertos se haya habilitado en su enrutador o firewall y tenga habilitados los servidores en su red privada.

## Escaneo completo
```Bash
nmap -p- -sCV -sS -O --open -T5 --min-rate 5000 -vvv -n -Pn  10.10.106.229 -oN Escaneo.txt
```

## Escaneo silencioso
```Bash
nmap -T0 -Pn -f -n -sV [IP]
```

## Detección sistema operativo
```Bash
nmap -Pn -O [IP]
```

## Escaneo rapido
```Bash
nmap -sC -sV [IP] -oN escaneo.txt
```

# Comprobación vulnerabilidad
```Bash
nmap --script ftp* -p 21 [IP]
```

## Escaneo puertos TCP y UDP
```Bash
nmap -p- -sU [ip]
```

## Escaneo host activos
```Bash
nmap -sn 192.168.1.0/24
```


------

## Escaneo red
```Bash
nmap 192.168.1.0/24
nmap 192.168.1.0-255
```

## Escaneo fragmentado especifica
```Bash
nmap -Pn -sS -sV -p80,445,3389 -f --mtu 32 [IP]
```

## Escaneo longitud de los datos
```Bash
nmap -Pn -sS -sV -p445,3389 -f --data-length 200 -D 10.10.10.1, 10.10.10.2 [IP]
```

## Escaneo ICMP
```Bash
nmap -sn -PE 192.168.1.6 --send-ip
```

Nota a apuntar, cuando un puerto especifico indique que no esta abierto ni cerrado, si la respuesta del puerto es filtrado es porque hay un firewall por medio






