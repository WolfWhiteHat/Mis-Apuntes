`DCDiag` es una herramienta de línea de comandos utilizada en entornos de Windows Server para diagnosticar problemas relacionados con controladores de dominio y la infraestructura de directorio activo. La herramienta se utiliza para realizar pruebas de diagnóstico en los controladores de dominio para detectar posibles problemas de configuración o funcionamiento.

Algunos de los aspectos que `DCDiag` puede evaluar incluyen la conectividad de red, la replicación entre controladores de dominio, la integridad de la base de datos de Active Directory, problemas de configuración DNS y otros aspectos críticos para el funcionamiento correcto de un entorno de directorio activo.


Para utilizar esta herramienta escribiremos el siguiente comando
```
dcdiag /s:<nombre_servidor> /v /c /e
```
![[Pasted image 20240918094701.png]]- `/s:<NombreDelServidor>`: Especifica el servidor que deseas probar.
- `/v`: Ejecuta DCDiag en modo detallado, proporcionando información más completa.
- `/c`: Realiza pruebas de conectividad.
- `/e`: Ejecuta todas las pruebas, incluyendo aquellas que normalmente se omiten.
- `/test:<NombreDeLaPrueba>`: Ejecuta una prueba específica en lugar de todas las pruebas.