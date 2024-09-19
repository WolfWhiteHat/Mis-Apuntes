Realizamos un escaneo con nmap
![[Pasted image 20240604072113.png]]

Encontramos el servicio 22, 139, 445 abiertos, comenzaremos escaneando mas a fondo el servicio smb. Realizamos una enumarecion de smb
![[Pasted image 20240604074850.png]]

Con enum4linux revisamos los permisos
![[Pasted image 20240604074932.png]]

Nos conectamos y obtenemos la primera flag, es lo unico que hemos obtenido del servicio smb
![[Pasted image 20240604075011.png]]
![[Pasted image 20240604075044.png]]

Revisamos el servicio NFS, con la utilizadad showmount podemos ver el directorio `/opt/conf`, creamos un directorio en /mnt para analizar la montura
![[Pasted image 20240604075445.png]]
![[Pasted image 20240604075749.png]]

Revisamos el directorio redis y encontramos un archivo de configuración de este servicio
![[Pasted image 20240604075857.png]]
![[Pasted image 20240604080054.png]]

Nos autenticamos en redis
```bash
redis-cli -a B65Hx562F@ggAZ@F -h 10.10.19.73 -p 6379
```
![[Pasted image 20240604080547.png]]

Revisamos la base de datos 0 y obtenemos la segunda flag
![[Pasted image 20240604080702.png]]

En Redis podemos ver el tipo de keys que existen con el siguiente comando
```Bash
type authlist
```
![[Pasted image 20240604081041.png]]

Vemos que authlist es un tipo de key de lista, así que podemos leer su valor con la siguiente función:
```Bash
lrange authlist 0 5
```
![[Pasted image 20240604081121.png]]

La clave esta en base 64, la descodificamos y obtenemos las credenciales de acceso al servicio rsync
![[Pasted image 20240604081310.png]]

Accedemos al servicio rsync y encontramos un directorio llamado files
![[Pasted image 20240604081518.png]]

Dentro de files encontramos un directorio del usuario sys-internal, accedemos a el
![[Pasted image 20240604081722.png]]

Encontramos un fichero .ssh por donde podriamos probar de explotar para obtener acceso por ahí, tambien encontramos la bandera de flag, revisamos el servicio ssh
![[Pasted image 20240604081936.png]]

Aparentemente no hay nada, ahora crearemos una clave de ssh y la subiremos
```Bash
ssh-keygen -f id_rsa
```
![[Pasted image 20240604082513.png]]

Renombramos la clave publica para subir el archivo a la maquina victima
![[Pasted image 20240604082730.png]]

Subimos la clave publica
![[Pasted image 20240604083027.png]]

Revisamos que se haya subido nuestra clave publica
![[Pasted image 20240604083053.png]]

Y ahora ya podriamos acceder por ssh y obtener acceso a la maquina victima
![[Pasted image 20240604083253.png]]

Ahora podemos ver la siguiente flag
![[Pasted image 20240604083343.png]]

Ahora vamos a buscar realizar una escalada de privilegios para obtener acceso como root, para empezar revisamos y en la carpeta raiz vemos una carpeta sospechosa
![[Pasted image 20240604084528.png]]

Leemos el fichero y parece que estan las explicaciones de como ejecutar el servicio
![[Pasted image 20240604084605.png|1500]]

Dentro de este documento de txt nos indica que este servicio corre por el puerto 8111 por defecto, lo revisamos con ss ya que no disponemos de netcat
```Bash
ss -tn
```
![[Pasted image 20240604085431.png]]

Antes de ejecutar el comando para realizar portforwarding con ssh, cambiaremos los permisos a nuestra clave privada
```Bash
chmod 600 id_rsa
```
![[Pasted image 20240604090115.png]]

Lo encontramos abierto, ahora para poder acceder necesitamos hacer portforwarding, para ello ejecutaremos el siguiente comando con ssh desde nuestra maquina atacante
```Bash
ssh -i id_rsa -L 8111:127.0.0.1:8111 sys-internal@10.10.19.73
```
![[Pasted image 20240604085834.png]]

Si ahora vamos al navegador veremos el servicio por el puerto que esta corriendo la maquina
![[Pasted image 20240604085955.png]]

Como podemos ver ya estamos dentro del servicio TeamCity, ahora para acceder si accedemos a as a Super User nos solicita un token
![[Pasted image 20240604091231.png]]

En la documentación de TeamCity especifica que el codigo se ubica en el archivo teamcity-server.log en la ruta de TeamCity\lgos
![[Pasted image 20240604091352.png]]

Al leer este fichero nos indica que no disponemos de permisos
![[Pasted image 20240604091434.png]]

Para ello ejecutaremos el siguiente comando para leer todos los ficheros y ver si encontramos algun token que podamos ver
```Bash
cat * | grep "token" 2>/dev/null
```
![[Pasted image 20240604091540.png]]

Probamos los 5 tokens a ver si podemos acceder con alguno de estos 5 tokens y accedemos al servicio
![[Pasted image 20240604092443.png]]

Crearemos un proyecto
![[Pasted image 20240604094315.png]]

Continuamos creando una build
![[Pasted image 20240604094440.png]]

Ahora dentro de la build nos deja modificarla y ejecutar comandos, añadimos el usuario sysinternal al grupo de root
```Bash
echo "sys-internal ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/sys-internal
```
![[Pasted image 20240604095449.png]]

Ejecutamos la build
![[Pasted image 20240604095030.png]]

Y ahora desde la terminal de SSH ya podriamos estariamos como root
![[Pasted image 20240604095520.png]]

Si ahora vamos a la carpeta `/etc/sudoers.d/` encontraremos que hemos añadido el usuario sys-internal
![[Pasted image 20240604100227.png]]

Y aqui tenemos el fichero de sudoers
![[Pasted image 20240604100124.png]]