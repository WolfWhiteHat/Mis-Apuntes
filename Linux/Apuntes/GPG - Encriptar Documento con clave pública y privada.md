En primer lugar, voy a utilizar dos máquinas virtuales, donde una será mi máquina ubuntu donde recibiré el documento encriptado; y la otra un Kali Linux, que será la que creará un documento que se enviará de forma encriptada a la máquina Ubuntu. Por tanto, en primer lugar vamos a crear un par de claves RSA en cada una de esta máquinas con el comando gpg –gen-key:
![[Mis apuntes/ANEXOS/image6.png]]
Después se nos pedirá que introduzcamos una contraseña:
![[Mis apuntes/ANEXOS/image7.jpeg]]
Y ahora debemos exportar la clave pública a un fichero de esta manera:
![[Mis apuntes/ANEXOS/image8.jpeg]]
Ahora vamos a enviar esta clave pública al equipo Kali Linux:
![[Mis apuntes/ANEXOS/image9.jpeg]]
Crearemos el fichero sad22.txt que será el fichero que vamos a encriptar y enviar a la máquina Ubuntu:
![[Mis apuntes/ANEXOS/dgdfghdfghdfg.png]]
Importamos la clave pública generada desde Ubuntu a nuestro Kali:
![[Mis apuntes/ANEXOS/image11.jpeg]]
Y ahora encriptamos el fichero desde mi máquina Kali Linux:
![[Mis apuntes/ANEXOS/image12.jpeg]]
En este punto ya podremos enviar el fichero encriptado a la máquina Ubuntu para desencriptarlo con la clave privada generada al principio con la máquina Ubuntu; y gracias a que la clave privada ya existe en esta máquina, podremos desencriptar el archivo:
![[Mis apuntes/ANEXOS/image13.jpeg]]
Y ya tendremos el archivo desencriptado:
![[Mis apuntes/ANEXOS/image14.jpeg]]
Por último, voy a listar las claves generadas de ambas máquinas con el comando gpg -k:
![[Mis apuntes/ANEXOS/image15.png]]
![[Mis apuntes/ANEXOS/image16.jpeg]]
