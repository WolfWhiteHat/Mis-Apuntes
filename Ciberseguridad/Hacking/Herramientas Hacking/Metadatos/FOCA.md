FOCA es un software de código abierto con el que podremos extraer los metadatos de cualquier tipo de documento (documentos de texto, imágenes, vídeos, etc.).
Foca proporciona una serie de herramientas y recursos para ayudar a las organizaciones a evaluar su seguridad cibernética, identificar vulnerabilidades y mitigar riesgos. Estas herramientas incluyen:

- Un escáner de vulnerabilidades
- Un analizador de malware
- Un sistema de detección de intrusiones
- Un sistema de gestión de eventos de seguridad
- Un conjunto de herramientas de respuesta a incidentes

# Tutorial instalacion
```
https://portafolio-aacm.onrender.com/cursos/hacking-etico/entradas/como-instalar-la-foca
```

# Requisitos de FOCA
![[Pasted image 20240205100835.png]]

# Instalar foca
Primero iremos al repositorio de FOCA en github
```
https://github.com/ElevenPaths/FOCA
```

Nos descargaremos el archivo zip de foca con su ultima versión
![[Pasted image 20240205100744.png]]

# Instalar C++
```
https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170
```
![[Pasted image 20240205101300.png]]

# Instalar SQL Server
```
https://www.microsoft.com/en-us/sql-server/sql-server-downloads
```

# Instalar .NET
```
https://dotnet.microsoft.com/en-us/download/dotnet-framework
```


---------

# Uso de FOCA
Vamos a descargar un documento aleatorio:
![[Pasted image 20231220111211.png]]

Lo descargamos y dejamos FOCA preparado para su uso:
![[Pasted image 20231220111240.png]]

Y en la parte de Document Analysis podemos añadir el fichero a analizar:
![[Pasted image 20231220111335.png]]

Y en la misma parte ya lo tenemos localizable:
![[Pasted image 20231220111419.png]]

Y ahora hacemos clic derecho sobre el fichero y le damos a extract metadata:
![[Pasted image 20231220111509.png]]

Y obtenemos los metadatos:
![[Pasted image 20231220111608.png]]

También podemos automatizar la descarga de muchos archivos de un target en específico creando un proyecto:
![[Pasted image 20231220111714.png]]

Y por aquí le pedimos a FOCA que nos busque por archivos:
![[Pasted image 20231220111801.png]]

Y nos encuentra los distintos documentos:
![[Pasted image 20231220111836.png]]

Podemos bajarnos documentos a la vez seleccionándolos y dando en descargar:
![[Pasted image 20231220111938.png]]

Los que están con el puntito verde es que están descargados:
![[Pasted image 20231220112036.png]]

Y sacamos los metadatos:
![[Pasted image 20231220112101.png]]

Y vemos los resultados, donde obtenemos usuarios y más cosas:
![[Pasted image 20231220112138.png]]
