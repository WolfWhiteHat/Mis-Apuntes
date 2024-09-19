# Actualizar e Instalar paquetes
```
sudo apt-update && sudo apt-upgrade -y
```

# Actualización mas completa
```
sudo apt dist-upgrade -y
```

# Eliminar paquetes inecesarios
```
sudo apt autoremove -y
```

# Deshabilitar servicios inecesarios
Listar servicios
```
systemctl list-unit-files | grep enable
```

Deshabilitar servicios
```
sudo systemctl disable <servicio>
```

# Configuración firewall
## **Instalar firewall ufw**
```
sudo apt install ufw
```

## **Bloquear todas las conexiones entrantes**
```
sudo ufw default deny incoming
```

## **Permitir todas las conexiones salientes**
```
sudo ufw default allow outgoing
```

## **Permitir conexiones SSH entrantes**
```
sudo ufw allow ssh
```

## **Activar firewall con todas las reglas configuradas**
```
sudo ufw enable
```

# Configurar SSH
## **Configurar ssh**
```
sudo nano /etc/ssh/sshd_config
```

## **Configuración fichero**
```Bash
Include /etc/ss/sshd_config.d/*.conf

#Port 2200
#Addressfamily any
#ListenAddess 0.0.0.0
#ListenAddress ::
```

## **Aplicar cambios**
```
sudo systemctl restart sshd
```

## **Usar clave publica para SSH**
### **Generar clave RSA**
```
ssh-keygen -t rsa -b 4096
```

### **Copiar clave al servidor**
```
ssh copy-id-usuario@tu-servidor
```

# Instalar VPN
## **ProtonVPN**
```
https://protonvpn.com/es-es
```

## **OpenVPN**
```
sudo apt install openvpn
```

```
sudo openvpn -config /path/to/your/config.ovpn
```

# Configurar DNS privados
```
sudo nano /etc/resolv.conf
```

## **Configuración fichero DNS**
```
nameserver 1.1.1.1
nameserver 1.0.0.1
```
