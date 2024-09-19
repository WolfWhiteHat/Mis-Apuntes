
Realizamos un escaneo de nmap y encontramos los puertos 22 y 80 abiertos
![[Pasted image 20240618083611.png]]

Encontramos el puerto 80 abierto, hacemos fuzzing para encontrar directorios y ficheros ocultos
![[Pasted image 20240618083652.png]]

Ahora realizamos una enumeración de usurarios por el puerto ssh
```
https://github.com/epi052/cve-2018-15473/tree/master
```
```Bash
./ssh-username-enum.py -t 10 -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt 10.10.226.3
```
![[Pasted image 20240618083904.png]]

Ahora con los usuarios encontrados realizaremos un ataque de fuerza bruta con hydra contra el panel de login
```Bash
hydra -l admin -P /home/wolf/rockyou.txt 10.10.226.3 http-post-form '/admin/:user=^USER^&pass=^PASS^:Username or password invalid'
```
![[Pasted image 20240618091849.png]]

Accedemos y ya obtenemos la flag de la web
![[Pasted image 20240618092148.png]]

Al acceder obtenemos la clave privada cifrada
![[Pasted image 20240618092940.png]]

Copiamos la clave privada en un archivo
![[Pasted image 20240618095607.png]]

Con la clave privada en un archivo la pasamos a texto plano con ssh2john
![[Pasted image 20240618094039.png]]

Ahora con john the ripper podemos intentar crackers la password
![[Pasted image 20240618094136.png]]

Una vez tenemos la clave utilizando el id_rsa y la password accederemos por ssh
![[Pasted image 20240618094718.png]]

Una vez obtenido el acceso ahora procederemos a obtener acceso a root, revisando los permisos de sudo encontramos que podemos usar cat sin la password de sudo
![[Pasted image 20240618101236.png]]

Intentamos leer el fichero de shadow y encontramos la contraseña de root cifrada
![[Pasted image 20240618101613.png]]

Guardamos el hash en un fichero
![[Pasted image 20240618103051.png]]

Y con john crackeamos el hash y obtenemos las credenciales
![[Pasted image 20240618103012.png]]

Al probarlo vemos que ya somos root
![[Pasted image 20240618103206.png]]



