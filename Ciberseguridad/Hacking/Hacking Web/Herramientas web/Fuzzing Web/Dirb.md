Dirb es un escáner de contenido web, también conocido como una herramienta de fuerza bruta para el descubrimiento de ficheros y directorios existentes en un portal web.
Funciona lanzando un ataque basado en diccionario contra un servidor web y analizando las respuestas devueltas por este.

Podemos utilizar dirb si queremos encontrar también extensiones de rutas. Es una herramienta de enumeración de directorios para identificar archivos y directorios ocultos en un sitio web. Funciona enviando solicitudes HTTP a un servidor web e identificando posibles rutas de acceso:
![[Mis apuntes/ANEXOS/Pasted image 20230210132531.png]]

Ahora otro ejemplo pero con un dominio, y vemos que funciona igual y nos encuentra varios directorios:
```Bash
dirb http://url
```
![[Mis apuntes/ANEXOS/Pasted image 20230218082716.png]]

Y vemos que la ruta assets existe:
![[Mis apuntes/ANEXOS/Pasted image 20230218082751.png]]
