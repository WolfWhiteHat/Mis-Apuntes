# CHKDSK:
CHKDSK es una herramienta de diagnóstico de disco incorporada en los sistemas operativos Windows que se utiliza para verificar la integridad del sistema de archivos y buscar y corregir errores en los discos duros y otros medios de almacenamiento. Algunas de las funciones principales de CHKDSK incluyen:

- **Verificar la integridad del sistema de archivos**: CHKDSK examina el sistema de archivos en busca de posibles problemas como sectores defectuosos, entradas de directorio dañadas o errores en la estructura del sistema de archivos.
- **Corregir errores del sistema de archivos**: Cuando CHKDSK encuentra errores en el sistema de archivos, intenta corregirlos automáticamente. Esto puede incluir la reasignación de sectores defectuosos, la eliminación de archivos huérfanos o la corrección de entradas de directorio incorrectas.
- **Recuperar datos legibles de sectores dañados**: Si CHKDSK encuentra sectores dañados en el disco, intenta recuperar la información legible de estos sectores y moverla a áreas de disco sin errores.
- **Mejorar el rendimiento del disco**: Al corregir errores en el sistema de archivos y eliminar problemas de fragmentación, CHKDSK puede ayudar a mejorar el rendimiento general del disco.

## **Comandos CHKDSK:**
- `chkdsk /f`: Corrige errores en el disco, incluyendo los encontrados en el sistema de archivos.
- `chkdsk /r`: Localiza sectores defectuosos y recupera la información legible.
- `chkdsk /x`: Desmonta el volumen antes de realizar una comprobación.

```
chkdsk /f /r
```


## **Eliminar particiones (diskpart)**

DiskPart es una herramienta de línea de comandos incorporada en los sistemas operativos Windows que se utiliza para administrar discos duros, particiones y volúmenes. Algunas de las funciones principales de DiskPart incluyen:

- **Listar discos**: Permite mostrar una lista de todos los discos disponibles en el sistema.
- **Seleccionar disco**: Permite seleccionar un disco específico para realizar operaciones en él, como crear particiones o cambiar el tipo de partición.
- **Listar particiones**: Muestra una lista de todas las particiones en el disco seleccionado.
- **Seleccionar partición**: Permite seleccionar una partición específica para realizar operaciones en ella, como cambiar el tamaño o eliminarla.
- **Crear partición**: Permite crear una nueva partición en el disco seleccionado.
- **Eliminar partición**: Permite eliminar una partición existente en el disco seleccionado.
- **Limpiar disco**: Elimina todos los datos y metadatos de particiones en el disco seleccionado, lo que permite volver a particionar el disco desde cero.
- **Convertir el tipo de partición**: Permite cambiar el tipo de partición entre MBR (Master Boot Record) y GPT (GUID Partition Table).
- **Extender partición**: Permite aumentar el tamaño de una partición existente para aprovechar el espacio no asignado en el disco.
- **Redimensionar partición**: Permite cambiar el tamaño de una partición existente, ya sea para hacerla más grande o más pequeña.

## **Comandos Diskpart**
- `diskpart`: Ejecuta el programa
- `list disk`: Muestra una lista de todos los discos disponibles en el sistema.
- `select disk [número]`: Selecciona un disco específico para realizar operaciones en él, donde [número] es el número del disco.
- `detail disk`: Muestra detalles específicos sobre el disco seleccionado, como el tamaño, el número de serie y el tipo de interfaz.
- `list partition`: Muestra una lista de todas las particiones en el disco seleccionado.
- `select partition [número]`: Selecciona una partición específica para realizar operaciones en ella, donde [número] es el número de la partición.
- `detail partition`: Muestra detalles específicos sobre la partición seleccionada, como el tamaño, el tipo de archivo y el estado.
- `create partition primary [size]`: Crea una nueva partición primaria en el disco seleccionado, donde [size] es el tamaño deseado de la partición en MB.
- `delete partition`: Elimina la partición seleccionada.
- `clean`: Elimina todos los datos y metadatos de particiones en el disco seleccionado.
- `convert mbr`: Convierte el disco seleccionado en un disco con tabla de particiones de estilo MBR (Master Boot Record).
- `convert gpt`: Convierte el disco seleccionado en un disco con tabla de particiones de estilo GPT (GUID Partition Table

https://www.youtube.com/watch?v=vkO688psBbE
