Es un editor hexadecimal que permite ver y modificar archivos a nivel binario. Esto significa que, con `hexedit`, puedes ver el contenido de un archivo en formato hexadecimal y realizar cambios directos en los bytes que lo componen.

# Instalación Hexedit
```
sudo apt install hexedit -y
```
![[Pasted image 20240906102625.png]]

Ahora para modificar un fichero `oneforall.jpg` ejecutamos el siguiente comando
```
hexedit oneforall.jpg
```

Esto es lo que nos aparece al abrir el fichero con hexedit, a la izquierda tenemos el desplazamiento o Offset, que es la posición del archivo, la culumna del centro nos muestra los datos en formato hexadecimal y a la derecha nos muestra los datos en ASCII
![[Pasted image 20240906105333.png]]

# Firma de archivos
Ahora modificaremos la firma de archivos.
Una **firma de archivo** o **magic number** es una secuencia específica de bytes que aparece al principio de un archivo y que identifica su tipo o formato. Estas firmas permiten que los sistemas operativos, herramientas de análisis de archivos, y otras aplicaciones identifiquen correctamente el tipo de archivo, incluso si la extensión (como `.jpg`, `.png`, `.exe`) es incorrecta o ha sido modificada.

## **Ejemplos de firmas de archivo:**
Aquí algunos ejemplos de firmas comunes:
- **JPEG (JPG)**: Los archivos JPEG comienzan con la secuencia `FF D8 FF`.
- **PNG**: Los archivos PNG empiezan con la secuencia `89 50 4E 47` (que corresponde al texto "PNG" en ASCII).
- **PDF**: Los archivos PDF empiezan con la secuencia `25 50 44 46` (que corresponde a "%PDF").
- **ZIP**: Los archivos ZIP comienzan con `50 4B 03 04`.

Estas firmas son útiles para muchas tareas, como el análisis forense de archivos, la recuperación de datos, o incluso para engañar a sistemas automatizados sobre el tipo de archivo (al modificar la firma).

En el siguiente enlace tenemos una lista de las firmas de archivos `file signature`
https://en.wikipedia.org/wiki/List_of_file_signatures?source=post_page-----ad58403aad4f--------------------------------

Buscamos en la web y encontramos los datos a modificar
![[Pasted image 20240906110003.png]]

Los modificamos
![[Pasted image 20240906110120.png]]

Y ahora lo volvemos a analizar con file
![[Pasted image 20240906110144.png]]

Realizado en la maquina [[MAQUINA U.A. High School Official v4 (Fuzzing web, injección de comandos desde navegador obteniendo reverse shell codificando paylaod, escalada de privilegios obteniendo password de fichero modificando firma de archivos y acceso a root explotandoeval)]]