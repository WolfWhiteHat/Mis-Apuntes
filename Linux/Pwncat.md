`pwncat` es una herramienta diseñada para simplificar y mejorar la interacción con conexiones de red, especialmente en el contexto de hacking ético y pruebas de penetración. Es esencialmente una versión mejorada de `netcat` (también conocido como `nc`), una herramienta de línea de comandos utilizada para leer y escribir datos a través de conexiones de red.
```
https://github.com/calebstewart/pwncat.git
```

# Instalacion Pwncat
## **Actualizamos el sistema**
```Bash
apt-get update && apt-get upgrade -y
```


Primero creamos una carpeta para el entorno virtual de pwncat
```
sudo mkdir pwncat
```
![[Pasted image 20240724144032.png]]

Ahora cambiamos el propietario de la carpeta
```
sudo chown $USER:$USER pwncat
```
![[Pasted image 20240724144012.png]]

Ahora creamos un entorno virtual
```
python3 -m venv pwncat_env
source pwncat_env/bin/activate
echo $VIRTUAL_ENV
```
![[Pasted image 20240724143056.png]]

Ahora instalamos pwncat
```
pip3 install pwncat
```
![[Pasted image 20240724144207.png]]

Verificamos la instalación
```
pwncat --version
```
![[Pasted image 20240724144328.png]]

Ahora para poder usar pwncat tendremos que activar el entorno virtual, para ello tenemos que indicarle la ruta completa donde esta el entorno virtual
```
source /opt/pwncat/pwncat_env/bin/activate
```
![[Pasted image 20240724144410.png]]

# Ejemplos pwncat
## **Escuchar con pwncat**
```
pwncat -l 4444
```
- `-l` indica que `pwncat` debe escuchar (listen).




