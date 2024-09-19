Realizamos un escaneo de nmap y encontramos varios puertos abiertos en los cuales por el 80 y por el 65524 corren dos webs
![[Pasted image 20240627081234.png]]

Revisamos la web que corre por el puerto 80 y encontramos los siguientes directorios
![[Pasted image 20240627091755.png]]

El archivo de robots.txt y no encontramos nada interesante
![[Pasted image 20240627081316.png]]

Accedemos al directorio encontrado en el puerto 80 y nos encontramos con la siguiente web
![[Pasted image 20240627094245.png]]

Volvemos ha hacer fuzzing web pero ahora del directorio encontrado
![[Pasted image 20240627095519.png]]

Accedemos al enlace encontrado y vemos la siguiente web
![[Pasted image 20240627094310.png]]

Inspeccionamos el codigo y encontramos lo siguiente
![[Pasted image 20240627094335.png]]

Analizamos el hash y encontramos la primera flag
![[Pasted image 20240627094635.png]]

Hacemos fuzzing web para encontrar directorios y archivos ocultos del servicio que corre por el puerto 65524
![[Pasted image 20240627092835.png]]

![[Pasted image 20240627095717.png]]

Revisando código encontramos otra flag
![[Pasted image 20240627094929.png]]

Revisamos el archivo de robots y ahora si que encontramos un hash
![[Pasted image 20240627082049.png]]

Lo analizamos
![[Pasted image 20240627100532.png]]

Hay una web donde podemos decodificar el archivo
https://md5hashing.net/hash/md5
![[Pasted image 20240627101305.png]]
![[Pasted image 20240627101228.png]]

En la pagina de debian encontramos el siguiente hash
```
ObsJmP173N2X6dOrAgEAL0Vu
```
![[Pasted image 20240627100054.png]]

Al decodificarlo en base 32 encontramos el directorio oculto
```
/n0th1ng3ls3m4tt3r
```
![[Pasted image 20240627103436.png]]

Al acceder nos encontramos con la siguiente pagina
![[Pasted image 20240627103521.png]]

Ahora revisamos la pagina y encontramos este codigo
![[Pasted image 20240627103555.png]]

Lo analizamos y encontramos el tipo de hash
![[Pasted image 20240627103634.png]]

Lo crackeamos con john the ripper
```
mypasswordforthatjob
```
![[Pasted image 20240627104804.png]]

Ya tenemos la password, revisando la pagina donde hemos encontrado la password tenemos una imagen
![[Pasted image 20240627105207.png]]

Nos la descargamos
![[Pasted image 20240627105227.png]]

Y ahora extraemos los metadatos con steghide y la contraseña obtenida previamente
```
username: boring
password: 01101001 01100011 01101111 01101110 01110110 01100101 01110010 01110100 01100101 01100100 01101101 01111001 01110000 01100001 01110011 01110011 01110111 01101111 01110010 01100100 01110100 01101111 01100010 01101001 01101110 01100001 01110010 01111001
```
![[Pasted image 20240627105703.png]]

Ahora tendremos que decodificar la password codificada en binario y obtenemos la password
```
iconvertedmypasswordtobinary
```
![[Pasted image 20240627110014.png]]

Probamos a acceder por ssh y ya estamos dentro
![[Pasted image 20240627110210.png]]

Leemos la bandera de user pero parece erronea
![[Pasted image 20240627110443.png]]

Decodificamos la flag
![[Pasted image 20240627112835.png]]

Revisamos y encontramos una tarea la cual parece interesante investigar
![[Pasted image 20240627111225.png]]

Revisamos las cron y encontramos que hay una tarea ejecutandose como root
![[Pasted image 20240627111631.png]]

Revisamos el fichero y encontramos que tenemos acceso de lectura y escritura
![[Pasted image 20240627111934.png]]

Modificamos el fichero y nos ponemos en escucha con netcat, ahora solo quedara esperar
![[Pasted image 20240627111858.png]]

Y ya somos root
![[Pasted image 20240627112016.png]]

Leemos la flag de root
![[Pasted image 20240627112912.png]]
