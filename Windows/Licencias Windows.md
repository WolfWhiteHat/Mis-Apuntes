• **OEM**: Más barata, vinculada al hardware, no transferible a otro equipo, generalmente preinstalada.
• **Retail**: Más cara, no vinculada al hardware, transferible entre equipos, puedes adquirirla y usarla en cualquier momento.
# Recuperar licencia después de restablecer equipo
Editor de registro
_HKEY _ LOCAL _ MACHINE / SOFTWARE / Microsoft / Windows NT / CurrentVersion / SoftwareProtectionPlatform
**BackupProductKeyDefault**

# Comandos CMD
## **Ver licencia activa**
```
wmic path softwarelicensingservice get OA3xOriginalProductKey
```

## **Borrar clave**
```
slmgr.vbs -upk
```

## **Ingresar nueva clave**
```
slmgr /ipk XXXXX-XXXXX-XXXXX–XXXXX–XXXXX
```

## **Activar clave**
```
slmgr/skms kms.digiboy.ir
```

## **Finalizar activación**
```
slmgr /ato
```

## **Verificar instalación**
```
slmgr /xpr
```

## **Windows activado PowerShell**
```
(Get-WmiObject -query ‘select * from SoftwareLicensingService’).OA3xOriginalProductKey
```

## **Información licencia**
```
slmgr /dlv
```