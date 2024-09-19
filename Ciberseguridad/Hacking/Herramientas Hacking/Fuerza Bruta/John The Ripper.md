John the Ripper es una herramienta para recuperación de contraseñas. 

# EXTRAER CONTRASEÑA FICHERO ZIP
Lo primero será ver todos los scripts que tiene esta herramienta; los veremos con el comando locate:
![[Mis apuntes/ANEXOS/Pasted image 20230206131400.png]]

Ahora vamos a hacer la prueba de crear un fichero .zip que tenga una contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230206131519.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230206133015.png]]

Y esto ya nos genera el archivo .zip con contraseña, pero si queremos ahora romper esa password con john the ripper, tenemos primero que extraer el hash de dicho fichero:
![[Mis apuntes/ANEXOS/Pasted image 20230206133114.png]]

Ahora ya podemos crackear el fichero hash.txt con el fin de desencriptar la password; lo cual lo haremos estos parámetros seleccionando un diccionario y el fichero .txt con el hash extraido:
![[Mis apuntes/ANEXOS/Pasted image 20230206133418.png]]

# OBTENER CONTRASEÑA FICHERO RAR

Lo primero será crear el fichero .rar con la contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230206133731.png]]

Y hacemos igual que antes, extraemos el hash de este fichero con john:
![[Mis apuntes/ANEXOS/Pasted image 20230206133823.png]]
Y de la misma forma que hicimos antes, hacemos el ataque de fuerza bruta contra este otro hash:
![[Mis apuntes/ANEXOS/Pasted image 20230206133912.png]]

# CRACKEAR HASHES CON JOHN THE RIPPER

Podemos también romper un hash con john the ripper, por ejemplo voy a romper este hash que contiene la password 123123 en md5 y sha1:
![[Mis apuntes/ANEXOS/Pasted image 20230206201408.png]]

Y vamos a ver que no hace falta proporcionar un diccionario porque John ya está utilizando uno por defecto:
![[Mis apuntes/ANEXOS/Pasted image 20230206201220.png]]

Haríamos lo mismo si quisiéramos hacerlo con un hash SHA:
![[Mis apuntes/ANEXOS/Pasted image 20230206201335.png]]

También podemos hacer esto mismo pero especificando un diccionario, por ejemplo el rockyou:
![[Mis apuntes/ANEXOS/Pasted image 20230509112204.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230509112320.png]]
# CRACKING HASHES BCRYPT
Bcrypt es un algoritmo de hashing de contraseñas diseñado para ser seguro y resistente a los ataques de fuerza bruta y diccionario. Se utiliza comúnmente para almacenar contraseñas de usuarios en bases de datos, protegiéndolas contra el acceso no autorizado.

Si queremos desencriptar un hash en formato bcrypt, lo haremos con el siguiente comando:
```bash
john --format=bcrypt --wordlist=rockyou.txt hash
```

O también podemos usar hashcat:
```bash
hashcat -m 1800 hash.txt rockyou.txt
```

# CRACKEAR KEEPAS CON JOHN THE RIPPER
También podemos crackear una base de datos de keepas con keepass2john, donde podemos ejecutar este comando:
```bash
keepass2john Database.kdbx > keepas.txt
```

Y a continuación, ya podemos crackear la base de datos con normalidad:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt keepas.txt
```
![[Mis apuntes/ANEXOS/Pasted image 20230911161834.png]]

Y efectivamente esta es la contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230911161853.png]]

# Cracking con ssh2john
Copiamos la clave privada en un archivo
![[Pasted image 20240618095607.png]]

Con la clave privada en un archivo la pasamos a texto plano con ssh2john
![[Pasted image 20240618094039.png]]

Ahora con john the ripper podemos intentar crackers la password
![[Pasted image 20240618094136.png]]

Una vez tenemos la clave utilizando el id_rsa y la password accederemos por ssh
![[Pasted image 20240618094718.png]]

[[MAQUINA BRUTE IT ( Fuzzing con gobuster, captura de panel de login con burpsuite para posteriormente realizar un ataque de fuerza bruta con hydra, transferir id_rsa privada a texto plano para crackerla, escalada de privilegios con permisos de sudo cat)]]


# Cracking con zip2hohn
Con zip2john extraemos la información de hash de contraseñas almacenadas en archivos ZIP protegidos con contraseña
![[Pasted image 20240628120330.png]]

[[MAQUINA AGENT SUDO (UserAgent Burpsuit, esteganografía con binwalk, steghide y foremost, cracking con zip2john y escalada de privilegios con vulnerabilidad de linux exploit suggester)]]


# Cracking hashes NTLM
Para crackear la password de NTLM podemos copiar y pegar los datos como los hemos obtenido del sistema, con el usuario y el hash LM
```
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240722101320.png]]

Una vez obtenidas las password podemos volver a verlas descifradas con el siguiente comando
```
john --show hash.txt
```
![[Pasted image 20240722120442.png]]