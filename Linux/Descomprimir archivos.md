
# Comprimir y descomprimir .tar.gz .tar.z .tgz (tar con gzip)

## **Comprimir archivo tar.gz**
```Bash
tar -czvf archivo.tar.gz /ruta_destino
```

## **Descomprimir archivo tar.gz**
```Bash
tar -xzvf archivo.tar.gz
```

# Tar
`tar` es una herramienta de archivado que se utiliza comúnmente en sistemas basados en Unix para comprimir y descomprimir archivos y directorios.
## **Comandos**
- `x`: Extraer archivos de un archivo tar. Se utiliza junto con la opción `-f` para especificar el archivo tar.
- `c`: Crear un nuevo archivo tar. Se utiliza junto con la opción `-f` para especificar el nombre del archivo tar.
- `t`: Mostrar el contenido de un archivo tar.
- `v`: Modo verbose, muestra los archivos a medida que se procesan.
- `f`: Especifica el nombre del archivo tar.

## **Descomprimir archivo tar**
```Bash
tar xvf archivo.tar
```

## **Comprimir archivo tar**
```Bash
tar cvf archivo.tar /archivo/carpeta/*
```

## **Extraer archivos de un archivo tar**
```Bash
tar xf archivo.tar
```

## **Crear un nuevo archivo tar**
```Bash
tar cf nuevo_archivo.tar archivo1 archivo2 directorio1
```

## **Mostrar el contenido de un archivo tar**
```Bash
tar tf archivo.tar
```

# Zip
Resumen: `zip` es una utilidad de compresión de archivos muy popular en sistemas Unix y Linux.

## **Comandos**
- `x`: Extraer archivos de un archivo zip. Se utiliza para descomprimir el contenido del archivo zip.
- `c`: Crear un nuevo archivo zip. Se utiliza para comprimir archivos y directorios en un archivo zip.
- `v`: Modo verbose, muestra los archivos a medida que se procesan.
- `f`: Especifica el nombre del archivo zip.
- `d`: Eliminar archivos de un archivo zip.

## **Descomprimir archivo zip**
```Bash
unzip archivo.zip
```

## **Comprimir archivo zip**
```Bash
zip archivo.zip /carpeta/archivos
```

## **Crear un nuevo archivo zip**
```Bash
zip nuevo_archivo.zip archivo1 archivo2 directorio1
```

## **Extraer archivos con modo verbose**
```Bash
unzip -v archivo.zip
```

## **Eliminar archivos de un archivo zip**
```Bash
zip -d archivo.zip archivo1 archivo2
```

# Gzip
Resumen: `gzip` es una utilidad de compresión de archivos que se utiliza comúnmente en sistemas Unix y Linux.

## **Comandos**
- `d`: Descomprimir un archivo gzip.
- `r`: Modo recursivo, comprime directorios y sus contenidos.
- `v`: Modo verbose, muestra los archivos a medida que se procesan.
- `f`: Forzar la compresión o descompresión, incluso si el archivo ya existe.

## **Descomprimir archivo gzip**
```Bash
gzip -d archivo.gz
```

## **Comprimir archivo gzip**
```Bash
gzip -q directorio
```

## **Descomprimir con modo verbose**
```Bash
gzip -dv archivo.gz
```


# Bzip2
Resumen: `bzip2` es otra herramienta de compresión de archivos disponible en sistemas Unix y Linux.
## **Comandos**
- `d`: Descomprimir un archivo bzip2.
- `v`: Modo verbose, muestra los archivos a medida que se procesan.
- `f`: Forzar la compresión o descompresión, incluso si el archivo ya existe.

## **Descomprimir un archivo bzip2**
```Bash
bzip2 -d archivo.bz2
```

## **Comprimir archivo bzip2**
```Bash
bzip2 archivo
```

## **Descomprimir con modo verbose**
```Bash
bzip2 -dv archivo.bz2
```

# XZ
Resumen: `xz` es una herramienta de compresión de archivos con una alta tasa de compresión disponible en sistemas Unix y Linux.

## **Comandos**
- `d`: Descomprimir un archivo XZ.
- `v`: Modo verbose, muestra los archivos a medida que se procesan.
- `f`: Forzar la compresión o descompresión, incluso si el archivo ya existe.


## **Descomprimir un archivo XZ**
```Bash
xz -d archivo.xz
```

## **Comprimir un archivo**
```Bash
xz archivo
```

## **Descomprimir con modo verbose**
```Bash
xz -dv archivo.xz
```


