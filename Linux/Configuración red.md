Empezamos configurando las tarjetas de red en UTM
![[Pasted image 20240704133405.png]]
![[Pasted image 20240704133411.png]]

Ahora iniciamos la maquina de kali linux y configuramos las ip de red
```
sudo nano /etc/network/interfaces
```
![[Pasted image 20240704133735.png]]

Verificamos la conectividad
![[Pasted image 20240704135356.png]]

Revisamos la configuración del servidor DNS
![[Pasted image 20240704135556.png]]

Comprobamos que pueda resolver nombres de dominio
![[Pasted image 20240704135625.png]]

# Mostrar estado interfaces de red
![[Pasted image 20240704135745.png]]

# Mostrar tabla de enrutamiento
![[Pasted image 20240704135807.png]]

# Verificar estado servicio de red
```
systemctl status networking.service
```
![[Pasted image 20240704135921.png]]

# Registros servicios de red
```
journalctl -xeu networking.service
```
![[Pasted image 20240704140239.png]]


# Renovar configuracion DHCP
```
ifdown eth0
ifup eth0
```

# Verificar configuración de red
```
nmcli device show
```
![[Pasted image 20240704141653.png]]
# Verificar conexión de red
```
nmcli connection show
```
![[Pasted image 20240704141717.png]]
# Logs
/var/log/syslog
/var/log/auth.log
