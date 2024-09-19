**Impacket** es una colección de herramientas en Python utilizadas para interactuar con protocolos de red de bajo nivel, como TCP/UDP, SMB, LDAP, etc. Está diseñada para permitir a los desarrolladores y a los profesionales de la seguridad realizar tareas de auditoría y pruebas de penetración de sistemas y redes. Impacket proporciona implementaciones de protocolos específicos que permiten la manipulación de paquetes de red, lo que es crucial para diversas actividades de seguridad informática, incluyendo la explotación de vulnerabilidades, la auditoría de sistemas y la simulación de ataques.

# **Instalación Impacket**
Clonamos el repositorio en `/opt`
```
git clone https://github.com/SecureAuthCorp/impacket.git /opt/impacket
```
![[Pasted image 20240716125537.png]]

# **Configuración entorno virtual**
Para poder crear un entorno virtual es necesario instalar el paquete `python3.11-venv`
```
sudo apt install python3.11-venv
```
![[Pasted image 20240716130020.png]]

Dentro de la carpeta de impacket ejecutamos los siguientes comandos
```
python3 -m venv venv
source venv/bin/activate
```
![[Pasted image 20240716125923.png]]

# Instalamos las dependencias
```
sudo pip instal .
```
![[Pasted image 20240716130528.png]]

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

# Verificar instalación
Ahora para verificar la instalación podemos ejecutar cualquiera de los programas y revisar que el sistema los detecte como en la siguiente captura
![[Pasted image 20240716130923.png]]

Ejecutando otro programa de impacket
![[Pasted image 20240716131028.png]]

Como vemos a la derecha de las capturas estamos dentro del entrono virtual, ahora todo lo que trabajemos estara aislado del sistema, para ello instalaremos las dependencias de impacket
```
sudo pip install impacket
```
![[Pasted image 20240716133904.png]]

# Activar entorno virtual
```
source /opt/impacket/venv/bin/activate
```
![[Pasted image 20240716134137.png]]
# Desactivar entorno virtual
Como podemos ver con el siguiente comando lo desactivamos y si revisamos a la derecha desaparece el entorno virtual de impacket
```
deactivate
```
![[Pasted image 20240716134200.png]]


----
Todas las herramientas de impacket vienen por defecto instaladas en kali linux, para ejecutarlas tenemos que usar el prefijo de impacket
```
impacket-psexec Administrator@spookysec.local -hashes aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc
```
![[Pasted image 20240717113302.png]]

```
impacket-secretsdump -just-dc backup@10.10.143.170
```
![[Pasted image 20240717112613.png]]