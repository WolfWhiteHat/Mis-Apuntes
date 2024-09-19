DNS es un sistema que se utiliza para traducir los nombres de dominio legibles por humanos, como www.ejemplo.com, en direcciones IP (Protocolo de Internet) numéricas. 

-------------------------

Podemos realizar también consultas DNS para obtener información sobre nombres de dominio o para traducir un nombre de dominio en una dirección IP correspondiente de las siguientes formas:

# NSLOOKUP
```bash
nslookup www.google.es
```
![[Mis apuntes/ANEXOS/Pasted image 20230917125148.png]]
- La dirección IP de www.google.es es 142.250.184.3
- El servidor DNS donde hicimos la consulta es 192.168.0.1

# CONSULTA DE NSLOOKUP A SERVIDOR EXTERNO
Podemos también realizar una consulta DNS a un servidor externo en lugar de a nuestro servidor DNS local:
```bash
nslookup www.google.es 1.1.1.1
```
![[Mis apuntes/ANEXOS/Pasted image 20230917125405.png]]

Otros servidores externos útiles pueden ser:
1.1.1.1 Cloudflare
1.0.0.1 Cloudflare
8.8.8.8 Google
8.8.4.4 Google
9.9.9.9 Quad9
9.9.9.10 Quad9
209.244.0.3 Level3
209.244.0.4 Level3
208.67.222.222 OpenDNS
208.67.220.220 OpenDNS


## **Registros DNS**
- `A (Address Record)`: Asocia un nombre de dominio con una dirección IP IPv4.
- `AAAA (IPv6 Address Record)`: Similar al registro A, pero para direcciones IP IPv6.
- `CNAME (Canonical Name Record)`: Asocia un nombre de dominio con otro nombre de dominio (alias).
- `MX (Mail Exchange Record)`: Especifica los servidores de correo electrónico responsables de recibir correo para un dominio particular.
- `TXT (Text Record)`: Se utiliza para almacenar texto arbitrario asociado con un nombre de dominio. A menudo se usa para incluir información legible por humanos, como registros SPF o DKIM para el correo electrónico, o para verificar la propiedad del dominio.
- `NS (Name Server Record)`: Indica los servidores de nombres autorizados para un dominio específico.
- `PTR (Pointer Record)`: Utilizado para la resolución inversa de direcciones IP a nombres de dominio (como buscar el nombre de dominio asociado con una dirección IP).
- `SRV (Service Record)`: Se utiliza para describir los servicios disponibles en un dominio específico.
- `SOA (Start of Authority Record)`: Contiene información sobre el servidor de nombres autoritativo para el dominio, el administrador del dominio y otros metadatos de la zona.