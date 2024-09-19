
Si queremos realizar busquedas mas precisas, encontrar información que podria ayudarnos posteriormente a realizar una prueba de penetración podemos utilizar google dorks o también llamada google hacking.


### Comandos Google Dorks
#### SITE
Si escribimos site:ine.com, es decir la URL como podemos ver solo nos mostrara resultados de enlaces que contengan esa dirección y sus subdominios
site:ine.com
![[Pasted image 20240313100056.png|500]]

#### INURL
Con la opción inurl realizamos una busqueda mas exaustiva y podremos añadir alguna palabra la cual en los resultados solo nos aparecer url las cuales contengan esta palabra
site:ine.com inurl:admin
![[Pasted image 20240313100139.png|500]]

#### site:.ine.com
Escribiendo un ** delante del dominio nos buscara los subdominios que pueda tener el dominio
site:**.ine.com
![[Pasted image 20240313100301.png|500]]

#### INTITLE
Añadiendo el siguiente parametro unicamente nos mostrara las url que contengan la palabra admin en el titulo real del sitio
site:**.ine.com intitle:admin
![[Pasted image 20240313100416.png|500]]

#### Filetype
Añadiendo la siguiente función nos mostrara los dominios los cuales tengan algun documento especifico que busquemos
site:ine.com filetype:pdf
![[Pasted image 20240313100505.png|500]]
#### Palabra clave
Añadiendo una palabra clave nos buscara las páginas que contengan esta información y dentro de la propia URL contengan la palabra
site:ine.com employees
![[Pasted image 20240313100610.png|500]]


#### Index of
Utilizando la siguiente sintaxis podemos encontrar una vulnerabilidad de algunas paginas web el resultado nos mostrara direcciones y archivos públicos, es decir que no están ocultos en los cuales podremos obtener información sobre los servidores
intitle:index of
![[Pasted image 20240313100706.png|500]]



#### Cache
Con la siguiente función podremos buscar versiones anteriores de una URL, las empresas suelen realizar cambios de una web y de esta forma nos pueden mostrar alguna versión anterior, cuando insertamos el comandos nos accede directamente a la página web
cache:ine.com
![[Pasted image 20240313100758.png]]
![[Pasted image 20240313100819.png]]


#### Waybackmachine
Es una página web la cual nos muestra todo el historial de la URL que especifiquemos y que podremos ver como se veia en ese momento
https://archive.org/web/



#### Ejemplos
Realizando busquedas mas precisas podremos obtener información sobre direcciones que las empresas pueden pensar que estan ocultas y realmente es información que tienen compartida publicamente como puede ser los archivos de los servidores donde se ubican los usuarios o las contraseñas




#### URL Kali Linux BD
La empresa de Kali Linux tiene una URL con comandos utiles para realizar busquedas precisas de información que pueda ser sensible
https://www.exploit-db.com/google-hacking-database



