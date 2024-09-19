# Instalación paquete
Para poder crear un entorno virtual es necesario instalar el paquete `python3.11-venv`
```
sudo apt install python3.11-venv
```
![[Pasted image 20240716130020.png]]

# **Configuración entorno virtual**
Dentro de la carpeta donde queremos tener el entorno virtual ejecutamos los siguientes comandos
```
python3 -m venv venv
source venv/bin/activate
```
![[Pasted image 20240716125923.png]]
- **`-m venv`**: La opción `-m` le dice a Python que ejecute el módulo `venv` como un script. El módulo `venv` es utilizado para crear entornos virtuales.
- **`venv`**:Este es el nombre del directorio donde se creará y almacenará el entorno virtual.

# Añadir /opt/impacket al PATH
Accedemos al fichero `.zshrc` y agregamos la siguiente linea para poder ejecutar los programas desde cualquier lugar del sistema
```
export PATH="$PATH:/opt/impacket"
```
![[Pasted image 20240716130741.png]]

Cargamos la configuración
```
source ~~/.zshrc
```
![[Pasted image 20240716130822.png]]


# Activar entorno virtual
```
source app/venv/bin/activate
source /opt/impacket/venv/bin/activate
source /opt/pwncat/pwncat-env/bin/activate
```
![[Pasted image 20240716134137.png]]

# Desactivar entorno virtual
Como podemos ver con el siguiente comando lo desactivamos y si revisamos a la derecha desaparece el entorno virtual de impacket
```
deactivate
```
![[Pasted image 20240716134200.png]]

# Verificar si estamos ejecutando un entorno virtual
```
echo $VIRTUAL_ENV
```
![[Pasted image 20240724140534.png]]