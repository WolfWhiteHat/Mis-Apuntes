Es una herramienta que se utiliza para inyectar código malicioso en archivos ejecutables, generalmente con el propósito de evadir la detección de antivirus y realizar ataques.
Shellter es una aplicación de 32 bits diseñada para ejecutarse en sistemas operativos Windows de 32 bits. Cuando intentas ejecutar Shellter en un sistema Linux utilizando Wine, Wine necesita tener acceso a las bibliotecas y dependencias de 32 bits para que pueda funcionar correctamente.
# Instalar shellter
```
apt-get install shellter -y
```
![[Pasted image 20240503085644.png|1000]]


Para poder utilizar esta herramienta necesitamos tener instalado wine y habilitar la ejecución de programas de 32 bits
El comando `sudo dpkg --add-architecture i386` se utiliza en sistemas basados en Debian y sus derivados (como Ubuntu) para añadir la arquitectura de 32 bits (i386) al sistema. Esto es útil cuando estás trabajando en un sistema de 64 bits pero necesitas ejecutar aplicaciones o instalar paquetes diseñados para sistemas de 32 bits.

Cuando ejecutas este comando con `sudo` (que otorga permisos de superusuario), estás autorizando a `dpkg` (el gestor de paquetes de Debian) a añadir la arquitectura de 32 bits al sistema, lo que te permite instalar y ejecutar programas de esa arquitectura. Esto es útil en situaciones donde necesitas compatibilidad con software o librerías diseñadas específicamente para sistemas de 32 bits en un sistema de 64 bits.
```
sudo dpkg --add-architecure i386
```
![[Pasted image 20240503090103.png]]

```
sudo apt-get install wine32
```
![[Pasted image 20240503090523.png]]

Una vez instalado todo lo necesario accederemos al directorio donde se almacena el ejecutable de shellter
`/usr/share/windows-resources/shellter`
![[Pasted image 20240503094444.png]]

Una vez dentro del directorio ejecutaremos shellter con wine
```
sudo wine shellter.exe
```
![[Pasted image 20240503094602.png]]

Ahora seleccionamos la opcion a y posteriormente indicamos la ruta del archivo el cual queremos ejecutar en la maquina victima
![[Pasted image 20240503095325.png]]

La siguiente opción nos indica si queremos que ejecute el binario a parte del codigo malicioso que vamos a indicar, esto es recomendable activarlo para pasar desapercibido, la siguiente opción es para seleccionar que payload queremos cargar
![[Pasted image 20240503095729.png|500]]


Ahora seleccionamos el puerto y la IP que queremos que conecte, en este caso la de nuestra maquina
![[Pasted image 20240503095915.png]]

Una vez ha terminado de ejecutarse el programa ya tendremos el binario preparado, el archivo que antes era el binario ahora es el payload y el propio programa de shellter almacena una copia en su carpeta `Shellter_Backups`de esta forma podremos reutilizar el binario


Ahora solo quedaria ejecutar en la maquina victima, para ello cargamos un servidor de python con el archivo y nos ponemos en oyente con nuestra maquina
![[Pasted image 20240503100419.png]]

Descargamos el binario en windows
![[Pasted image 20240503100506.png]]

Y ahora al ejecutarlo actua como el propio visor de vnc pero conteniendo nuestra codigo para obtener una reverse shell
![[Pasted image 20240503100628.png]]

Si volvemos a nuestra maquina podemos ver que ya hemos obtenido la reverse shell de meterpreter
![[Pasted image 20240503100817.png]]

# Ruta binarios Windows
`/usr/share/windows-binaries/
![[Pasted image 20240503094858.png]]