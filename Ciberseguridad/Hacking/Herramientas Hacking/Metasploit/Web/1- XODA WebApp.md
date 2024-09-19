XODA es un sistema de gestión de documentos y archivos que ofrece una interfaz web para organizar, compartir y colaborar en documentos y archivos en línea. El nombre "XODA" es un acrónimo de "XO Document Archive".

Entre sus características principales se incluyen:

1. **Interfaz web intuitiva**: XODA proporciona una interfaz fácil de usar que permite a los usuarios navegar por los archivos y documentos almacenados en el sistema.
    
2. **Gestión de archivos y documentos**: Permite cargar, descargar, eliminar y organizar documentos y archivos en una estructura de carpetas.
    
3. **Colaboración**: Facilita la colaboración en documentos permitiendo a varios usuarios acceder y editar los mismos archivos simultáneamente.
    
4. **Control de versiones**: XODA puede realizar un seguimiento de las diferentes versiones de un documento, lo que facilita la revisión y restauración de versiones anteriores si es necesario.
    
5. **Seguridad**: Proporciona opciones para controlar el acceso a los documentos y archivos mediante la autenticación de usuarios y la asignación de permisos.


Realizamos un escaneo simple para ver los servicios abiertos
![[Pasted image 20240321084320.png]]

# Curl a ip de servidor
El puerto 80 esta abierto, eso significa que tiene una pagina web, para poder listar y revisar el codigo para obtener información podemos ejecutar el siguiente comandos
curl [IP]
![[Pasted image 20240321084521.png]]

Como podemos ver desde el codigo que hemos listado vemos que tiene la webapp de xoda, listamos los modulos y encontramos uno
![[Pasted image 20240321084834.png]]

Configuramos el modulo
![[Pasted image 20240321084936.png]]
![[Pasted image 20240321085322.png]]

