# GPO
Directiva de seguridad local -> secpol.msc
Actualizar politicas de grupo -> gpupdate /force
Permisos escriotorio remoto -> sysdm.cpl
Administrador directivas de seguridad -> GPMC.msc

UAC es el mensaje que aparece cuando solicita permisos de adminitrador para realizar cambios del sistema.


# UAC
UAC (User Account Control) es una característica de seguridad integrada en los sistemas operativos Windows, como Windows Vista, Windows 7, Windows 8, Windows 8.1 y Windows 10. El propósito principal de UAC es proteger el sistema al prevenir cambios no autorizados realizados por programas maliciosos o usuarios no autorizados.

Cuando UAC está activado, cada vez que se realiza una acción que requiere permisos de administrador, como instalar software, realizar cambios en la configuración del sistema o modificar archivos en ciertas áreas protegidas del sistema, Windows solicita una confirmación o una contraseña de administrador antes de permitir que la acción continúe. Esto ayuda a evitar que programas maliciosos realicen cambios sin el conocimiento o el consentimiento del usuario.

En resumen, UAC es una capa de seguridad diseñada para proteger el sistema operativo Windows al solicitar permiso antes de realizar acciones que podrían afectar la estabilidad o seguridad del sistema.

https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works

# Desactivar UAC

## **Metodo 1**
Dentro del editor de registro
Equipo\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA

## **Metodo 2**
Directivas de seguridad local
Directivas locales\Opciones de seguridad\Control de cuentas de usuario: ejecutar todos los administradores en Modo de aprobación de administrador