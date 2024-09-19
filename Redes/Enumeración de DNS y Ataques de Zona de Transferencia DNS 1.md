# Enumeración DNS
La enumeración de DNS es el proceso de recopilación de información (Information Gathering) sobre un dominio específico, que incluye la obtención de registros DNS públicos y privados asociados con ese dominio. Esto se realiza para obtener un panorama completo de la infraestructura de red de un dominio y puede ser utilizado tanto con fines legítimos (como la administración de sistemas) como con fines maliciosos (como la realización de ataques cibernéticos).

# Ataque de Zona de Transferencia DNS (AXFR)
Los ataques de Zona de Transferencia DNS (AXFR) son una forma de ataque donde un atacante intenta obtener una copia completa y exhaustiva de la base de datos de zona DNS de un dominio. Esto se logra explotando una debilidad en la configuración del servidor DNS que permite solicitudes de transferencia de zona sin autenticación adecuada. Los atacantes utilizan esta técnica para obtener información sensible, como nombres de host, direcciones IP y otros registros DNS, que pueden ser utilizados para realizar ataques más avanzados, como ataques de suplantación de identidad, ingeniería social o ataques de denegación de servicio (DoS).

# Diferencias
La principal diferencia entre la enumeración de DNS y los ataques de Zona de Transferencia DNS radica en el propósito y la legalidad de la actividad. La enumeración de DNS se realiza típicamente como parte de procesos de administración de sistemas y seguridad para comprender la infraestructura de red y prevenir vulnerabilidades. Por otro lado, los ataques de Zona de Transferencia DNS son técnicas maliciosas utilizadas por los atacantes para obtener información confidencial de manera no autorizada, lo que puede conducir a acciones adversas contra el sistema o la red objetivo.

# Registros DNS
- `SOA (Start of Authority)`: Este registro especifica la información sobre el servidor DNS principal responsable de un dominio particular. Contiene detalles como el nombre del servidor primario, el correo del administrador y detalles de tiempo de vida de los registros.
    
- `NS (Name Server)`: Indica los servidores de nombres autorizados para el dominio. Estos servidores de nombres resuelven consultas DNS de clientes en nombre del dominio.
    
- `A (Address)`: Este registro mapea un nombre de dominio a una dirección IP IPv4 correspondiente. Es el registro más común utilizado para resolver nombres de host a direcciones IP.
    
- `PTR (Pointer)`: Realiza el mapeo inverso de un dirección IP a un nombre de dominio. Es utilizado principalmente en búsquedas inversas DNS.
    
- `CNAME (Alias)`: Proporciona un alias a otro nombre de dominio. Se utiliza para asociar múltiples nombres de dominio con el mismo recurso físico, lo que facilita la gestión y la flexibilidad de la red.
    
- `MX (Mail Exchanger)`: Este registro especifica los servidores de correo que son responsables de recibir el correo electrónico en nombre del dominio. Es crucial para la entrega de correo electrónico según el estándar SMTP.

# Herramientas enumeración DNS

## **Activo:**

- `dig`: Herramienta avanzada para realizar consultas DNS, que ofrece funcionalidades detalladas y personalizables, como consultas por tipo de registro y obtención de respuestas detalladas del servidor DNS.
    
- `dnsenum`: Similar a `dnsmap`, esta herramienta está diseñada para enumerar subdominios y recopilar registros DNS de manera exhaustiva, ofreciendo opciones para ajustar la profundidad de la enumeración.
    
- `dnsrecon`: Herramienta avanzada de enumeración DNS que permite la búsqueda de subdominios, la recolección de registros DNS y la detección de transferencias de zona no autorizadas, proporcionando una visión completa de la infraestructura de red.
    
- `nmap`: Aunque es conocido por su escaneo de puertos, `nmap` también puede realizar escaneos de enumeración DNS para descubrir servidores de nombres y registros asociados, siendo una herramienta multifuncional ampliamente utilizada en seguridad informática.


## **Pasivo:**

- `host`: Herramienta que permite realizar consultas DNS de manera sencilla, proporcionando información básica como direcciones IP y servidores de nombres.
    
- `nslookup`: Otra herramienta de consulta DNS que permite obtener información detallada sobre la resolución de nombres de dominio, incluyendo la resolución inversa y la búsqueda de servidores de nombres.
    
- `fierce`: Herramienta automatizada que realiza búsquedas exhaustivas de registros DNS, utilizando técnicas como la transferencia de zona y la búsqueda de subdominios para obtener una visión completa de la infraestructura de red de un dominio.
    
- `dnsmap`: Herramienta de escaneo de red que enumera servidores DNS y sus registros asociados, útil para descubrir subdominios y obtener información sobre la infraestructura de red de un dominio.


# Bibliografia
https://www.hostinger.es/tutoriales/comando-dig-linux
https://behacker.pro/que-es-la-enumeracion-dns/#Que_es_la_enumeracion_DNS
https://www.welivesecurity.com/la-es/2015/06/17/trata-ataque-transferencia-zona-dns/
