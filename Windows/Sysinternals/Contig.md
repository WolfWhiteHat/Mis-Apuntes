Contig es una herramienta de línea de comandos de Sysinternals que te permite analizar y desfragmentar archivos individuales en sistemas Windows. A diferencia de la desfragmentación tradicional del disco, que reorganiza todo el contenido del disco, Contig se centra en archivos específicos, permitiéndote mejorar el rendimiento de aplicaciones que dependen de archivos grandes y fragmentados.

# Parametros Contig
- `archivo`: Especifica el archivo que se va a desfragmentar.
- `-a`: Desfragmenta todos los archivos en la carpeta y sus subcarpetas.
- `-b`: Desfragmenta el archivo y optimiza el uso del espacio en disco.
- `-c`: Realiza un análisis del archivo para mostrar el nivel de fragmentación sin realizar la desfragmentación.
- `-d`: Muestra el progreso detallado de la desfragmentación.
- `-e`: Desfragmenta los archivos que ya están optimizados, pero aún están fragmentados.
- `-f`: Desfragmenta los archivos grandes en la carpeta y sus subcarpetas.
- `-g`: Desfragmenta los archivos pequeños en la carpeta y sus subcarpetas.
- `-h`: Oculta archivos en el directorio de resultados.
- `-k`: Omite la confirmación de la desfragmentación de los archivos.
- `-l <tamaño>`: Especifica el tamaño del búfer de E/S en bytes. El valor predeterminado es 64 KB.
- `-n`: No imprime el encabezado o el resumen en la salida.
- `-o <archivo>`: Especifica el nombre del archivo de salida donde se escribirán los resultados.
- `-q`: Modo silencioso. No imprime mensajes en la salida.
- `-r`: Desfragmenta los archivos recursivamente en la carpeta y sus subcarpetas.
- `-s`: Desfragmenta todos los archivos del sistema, incluso los que están en uso.
- `-t`: Desfragmenta los archivos de tipo .tmp en la carpeta y sus subcarpetas.
- `-u`: Desfragmenta los archivos que ya están optimizados.
- `-v`: Versión. Muestra la información de versión de la herramienta.
- `-z`: Desfragmenta los archivos de tipo .sys en la carpeta y sus subcarpetas.

![[Pasted image 20240918095315.png]]