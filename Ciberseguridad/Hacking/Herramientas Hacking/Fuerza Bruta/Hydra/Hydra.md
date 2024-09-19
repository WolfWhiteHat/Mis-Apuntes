Hydra es conocida por su capacidad para realizar ataques de fuerza bruta contra una variedad de servicios, como SSH, HTTP, FTP, entre otros.

Comandos:
-   -f: termina la ejecución del comando si encuentra una posible clave valida.
- -l: Especifica un nombre de usuario para usar durante el ataque de fuerza bruta.
- -L: Especifica una lista de nombres de usuario para usar durante el ataque de fuerza bruta.
- -p: Especifica una contraseña para usar durante el ataque de fuerza bruta.
- -P: Especifica una lista de contraseñas para usar durante el ataque de fuerza bruta.
- -R: Restaura la versión anterior
- -s: Puerto específico
- -t: Selecciona el número de tareas a ejecutar
- -v: Este parámetro sirve para ver detalles en la salida de comando.
- -w: Especifica una lista de palabras para usar durante el ataque de fuerza bruta.
- -I: omite la espera inicial de 10 segundos y ver si hay algún mensaje de error o si el proceso se detiene en algún punto.

Las mayusculas y minusculas con l para el usuario y p para la contraseña se utiliza en minuscula cuando la sabemos y en minuscula cuando no

hydra 192.168.1.1 ftp -l msfadmin 
hydra -l admin -P rockyou.txt 192.168.1.1

# Tutorial Hydra
Primero accedemos al direcctorio donde estan los diccionarios
![[Pasted image 20240205125429.png]]

Como podremos ver en la siguiente imagen hydra viene con un diccionario muy amplio, en nuestro caso esta comprimido
![[Pasted image 20240205125307.png]]

Lo descomprimimos
![[Pasted image 20240205125357.png]]
Una vez descomprimido ejecutaremos el comando para que busque la pasword de un usuario de la maquina metasploitable 2

Como podemos ver una vez utilizado hydra y descubierto la contraseña, unicamente nos queda probarlo, nos conectamos por FTP a la maquina victima con las credenciales anteriormente descubiertas y ya acced
hydra 192.168.60.3 ftp -l msfadmin -P rockyou.txt -s 21
![[Pasted image 20240205141150.png]]


# Utilizar hydra protocolo SSH
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.50
![[Pasted image 20240226084922.png]]


# Password spray con Hydra
Podemos probar un ataque de rociado de contraseñas contra varios usuarios a ver si obtenemos unas credenciales y tenemos exito
```
hydra -L users.txt -p 'Th1s_1s_4_v3ry_s3cur3_p4ssw0rd' ssh://10.10.162.52
```
![[Pasted image 20240805090135.png]]