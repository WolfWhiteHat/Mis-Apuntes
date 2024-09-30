etwork Manager es una herramienta o servicio de software utilizado en sistemas operativos Linux para simplificar la configuración y administración de las conexiones de red. Su principal objetivo es facilitar a los usuarios y administradores la gestión de diferentes tipos de conexiones de red, como Ethernet (cableada), Wi-Fi (inalámbrica), banda ancha móvil (3G/4G), VPNs y más.


# **Características principales de Network Manager:**
• **Detección Automática:** Identifica automáticamente las redes disponibles y se conecta a ellas según las preferencias establecidas.
• **Gestión Unificada:** Proporciona una interfaz unificada para administrar todas las conexiones de red, eliminando la necesidad de configurar manualmente archivos de red.
• **Interfaces de Usuario:** Ofrece tanto interfaces gráficas (como nm-applet para entornos de escritorio) como herramientas de línea de comandos (como nmcli) para gestionar las conexiones.
• **Cambio Fluido entre Redes:** Permite cambiar fácilmente entre diferentes redes sin interrumpir la conexión o requerir reinicios del sistema.
• **Soporte para Configuraciones Avanzadas:** Admite configuraciones complejas, incluyendo proxys, servidores DNS personalizados, y ajustes de seguridad avanzados.


# Revisar servicio
```
systemctl status NetworkManager
systemctl start NetworkManager
systemctl stop NetworkManager
```

# Revisar interfaces
```
nmcli connect show
```

# Ruta configurar interfaces
```
/etc/NetworkManager/system-connections/
```

# Configurar interfaz
```Bash
nmcli connection add type ethernet ifname ens33 con-name Conexion_Estatica ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8 ipv4.method manual autoconnect yes
```

# Ejemplo interfaz
```
[connection]
id=ens34
uuid=4c138ad6-cd5f-4cb9-902e-283d5adf5e4f
type=ethernet
interface-name=ens33
autoconnect=true

[ipv4]
method=manual
addresses=192.168.1.100/24
gateway=192.168.1.1
dns=8.8.8.8;

[ipv6]
method=auto
```

# Configurar conexión DHCP
```
nmcli connection modify ens33 ipv4.method auto
nmcli connection up ens33
```

# Activar/Desactivar interfaz
```
nmcli connection up ens34
nmcli connection down ens34
```

# Exportar configuración
```
nmcli connection export Conexion_Estatica file Conexion_Estatica.nmconnection
```

# Importar configuración
```
nmcli connection import type file file Conexion_Estatica.nmconnection
```