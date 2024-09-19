Realizamos un escaneo sencillo
![[Pasted image 20240802075300.png]]

Ahora realizamos un escaneo mas completo
![[Pasted image 20240802075632.png]]

En el escaneo completo encontramos el nombre de la maquina, lo añadimos a nuestro `hosts`
![[Pasted image 20240802075619.png]]

Accedemos a la web que hay abierta en el puerto 80
![[Pasted image 20240802075733.png]]

Analizando la web encontramos los siguientes posibles usuarios
```
JD@anthem.com
Jane Doe
James Orchard Halliwell
```
![[Pasted image 20240802080113.png]]![[Pasted image 20240802080142.png]]
![[Pasted image 20240802080215.png]]

Ahora pasaremos a realizar fuzzing web y nos encuentra los siguientes directorios
![[Pasted image 20240802080725.png]]

Ahora pasamos a buscar a los directorios y revisar si encontramos algun archivo interesante, dentro del sitemap encontramos estas rutas
![[Pasted image 20240802080927.png]]

Revisando los directorios encontramos que al acceder a /umbraco encontramos el panel de login
```
http://10.10.232.216/umbraco/#/login
```

Analizando los archivos encontramos que podemos acceder a `robots.txt` en el cual encontramos una posible password y unos directorios ocultos
```
UmbracoIsTheBest!
```
![[Pasted image 20240802082554.png]]

En una de las paginas encontramos un poema
![[Pasted image 20240802085605.png]]

Si lo buscamos en internet nos aparece el autor, el cual podria ser un usuario del sistema
```
Solomon Grundy
```
![[Pasted image 20240802085639.png]]

Siguiendo la politica del usuario de JD, el usuario podria ser `SG`,  probramos a acceder con xfreerdp y obtenemos acceso al sistema
```
xfreerdp /u:sg /p:UmbracoIsTheBest! /v:10.10.232.216
```
![[Pasted image 20240802091524.png]]

Revisando como escalar privilegios encontramos que si mostramos los archivos ocultos encontramos un directorio con el nombre de `backup`
![[Pasted image 20240802092751.png]]

Al acceder encontramos un txt que al abrirlo nos muestra que no tenemos permisos
![[Pasted image 20240802092850.png]]
![[Pasted image 20240802092836.png]]

Intentamos cambiar los permisos del usuario y nos lo permite, ya tenemos acceso al documento
![[Pasted image 20240802093053.png]]

Dentro del txt encontramos una frase
```
ChangeMeBaby1MoreTime
```
![[Pasted image 20240802093202.png]]

Probamos a acceder con otra sesion como Administrator con esta password y obtenemos acceso
```
xfreerdp /u:Administrator /p:ChangeMeBaby1MoreTime /v:10.10.232.216
```
![[Pasted image 20240802093459.png]]






