Hacemos el escaneo con nmap y tiene el puerto 80 abierto:
![[Mis apuntes/ANEXOS/Pasted image 20230822095127.png]]
Y esto es lo que corre por el puerto 80:
![[Mis apuntes/ANEXOS/Pasted image 20230822095227.png]]
Ejecutando un whatweb vemos dos emails:
![[Mis apuntes/ANEXOS/Pasted image 20230822095532.png]]
Hacemos fuzzing y vemos varios directorios, como el de images:
![[Mis apuntes/ANEXOS/Pasted image 20230822095759.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230822095812.png]]
Donde vemos una especie de base de datos:
![[Mis apuntes/ANEXOS/Pasted image 20230822095853.png]]
De todos modos, en este fichero no encontraremos nada, por lo que viendo la web, tenemos un texto que leyéndolo de derecha a izquierda vemos que tiene un significado:
![[Mis apuntes/ANEXOS/Pasted image 20230822123614.png]]
```
No son estos hombres bien alimentados y con pelo largo los que temo, sino el pálido y el hambriento. cuatro es la referencia y la llave, suerte
```
El siguiente párrafo es posible que esté encriptado, por lo que investigamos en esta web:
```bash
https://www.dcode.fr/rot-cipher
```
![[Mis apuntes/ANEXOS/Pasted image 20230822125731.png]]
```bash
Para poder continuar el directorio vigenere deberas visitar ///http://url/VIGENERE/
```
Parece que eso está en VIGINERE:
![[Mis apuntes/ANEXOS/Pasted image 20230822130423.png]]
Y viendo el código fuente nos encontramos con otro texto extraño:
![[Mis apuntes/ANEXOS/Pasted image 20230822130504.png]]
En cyberchef podemos decodificar en vigenere poniendo la clave cuatro:
![[Mis apuntes/ANEXOS/Pasted image 20230822133435.png]]
Y lo mismo con la clave que estaba en el comentario:
![[Mis apuntes/ANEXOS/Pasted image 20230822133722.png]]
Todo esto nos debe dar la pista de r0n1n47:
![[Mis apuntes/ANEXOS/Pasted image 20230822134152.png]]
Ahora si hacemos fuzzing de este directorio, encontramos un robots.txt:
![[Mis apuntes/ANEXOS/Pasted image 20230822140636.png]]
Y vemos un nuevo directorio:
![[Mis apuntes/ANEXOS/Pasted image 20230822140704.png]]
Y nos encontramos con esto:
![[Mis apuntes/ANEXOS/Pasted image 20230822140729.png]]
Vemos que no nos deja descomprimir el archivo comprimido:
![[Mis apuntes/ANEXOS/Pasted image 20230822140802.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230822140914.png]]
Pero en el readme nos encontramos con la posible contraseña encriptada:
![[Mis apuntes/ANEXOS/Pasted image 20230822140942.png]]
