`netsh` es una herramienta que permite configurar prácticamente cualquier aspecto de las interfaces de red, firewalls y otras configuraciones relacionadas con la red.

# Cambiar configuración firewall
## **Deshabilitar firewall**
```
netsh advfirewall set allprofiles state off
```

## **Habilitar firewall**
```
netsh advfirewall set allprofiles state on
```

## **Permitir aplicación**
```
netsh advfirewall firewall add rule name="Allow MyApp" dir=in action=allow program="C:\path\to\myapp.exe" enable=yes
```

## **Permitir programa a traves del firewall**
```
netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80
```

# Configurar IP
```
netsh interface ip set address "Local Area Connection" static 192.168.1.100 255.255.255.0 192.168.1.1 1
```
