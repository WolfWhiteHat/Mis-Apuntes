vil-WinRM es una herramienta de código abierto diseñada para la administración remota de sistemas Windows mediante el protocolo WinRM (Windows Remote Management), pero con un enfoque más dirigido hacia la penetración y la seguridad de la red. Esta herramienta proporciona una interfaz de línea de comandos similar a PowerShell, que permite a los usuarios ejecutar comandos en sistemas Windows remotos de forma similar a como lo harían con PowerShell remoto, pero con algunas mejoras y simplificaciones para facilitar su uso en contextos de pruebas de penetración y auditoría de seguridad.

Entre las características de Evil-WinRM se incluyen:

1. Autenticación integrada: Puede autenticarse utilizando credenciales de usuario o utilizando hashes NTLM para mayor flexibilidad.
2. Soporte para canales cifrados: Puede establecer conexiones cifradas utilizando el protocolo HTTPS para una comunicación segura.
3. Interfaz de línea de comandos amigable: Proporciona una interfaz de línea de comandos fácil de usar, similar a PowerShell, que permite ejecutar comandos en sistemas Windows remotos.
4. Funciones adicionales: Además de la funcionalidad básica de administración remota, Evil-WinRM también incluye características adicionales, como la ejecución de scripts y la transferencia de archivos.

En resumen, Evil-WinRM es una herramienta útil para los profesionales de seguridad que necesitan realizar pruebas de penetración y auditorías en entornos que utilizan sistemas Windows, permitiendo la administración remota de manera efectiva y simplificada. Sin embargo, es importante tener en cuenta que debe utilizarse de manera ética y responsable, con permiso explícito para realizar pruebas en sistemas y redes que no son de su propiedad.


### Ejemplo
evil-winrm.rb -u administrator -p 'tinkerbell' -i 10.2.28.238
![[Pasted image 20240308125010.png]]