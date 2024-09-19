# Configurar y iniciar el servicio LicenseManager
Configuramos el servicio **LicenseManager** para que inicie automáticamente y luego lo inicia.
```
sc config LicenseManager start= auto & net start LicenseManager 
```

# Configurar y iniciar el servicio Windows Update (wuauserv)
Configuramos el servicio **wuauserv** (Windows Update) para que inicie automáticamente y luego lo inicia
```
sc config wuauserv start= auto & net start wuauserv 
```

# Configurar y iniciar el servicio Windows Update (wuauserv)
Cambiamos la clave de producto de Windows a la clave especificada
```
changepk.exe /productkey XXXXX-XXXXX-XXXXX–XXXXX–XXXXX
```
