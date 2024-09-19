Una ruta absoluta y una ruta relativa son formas de especificar la ubicación de un archivo o directorio en un sistema de archivos. Aquí están las diferencias entre ambas:

1. **Ruta Absoluta**:
    
    - Una ruta absoluta especifica la ubicación completa de un archivo o directorio desde la raíz del sistema de archivos.
    - Comienza desde el directorio raíz, que en sistemas basados en UNIX y Linux se representa como `/`, y en sistemas basados en Windows, se representa como una letra de unidad seguida de `:\`.
    - Un ejemplo de una ruta absoluta en sistemas basados en UNIX sería `/home/usuario/archivo.txt`, donde `/home` es el directorio raíz y `usuario/archivo.txt` es la ruta completa al archivo.
2. **Ruta Relativa**:
    
    - Una ruta relativa especifica la ubicación de un archivo o directorio en relación con el directorio actual.
    - No comienza desde la raíz del sistema de archivos; en su lugar, se basa en la ubicación del directorio desde el cual se está haciendo referencia.
    - Puede ser simplemente el nombre de un archivo o directorio si se encuentra en el directorio actual, o puede utilizar referencias a directorios padres (`..`) o subdirectorios (`./`).
    - Un ejemplo de una ruta relativa sería `../../directorio/archivo.txt`, donde `..` representa el directorio padre del directorio actual y `directorio/archivo.txt` es la ruta relativa al archivo.

# Ejemplo ruta
~ Se utiliza para especifira la ruta del usuario, si utilizamos el siguiente parametro:
~/les.sh --> /home/usuario/les.sh