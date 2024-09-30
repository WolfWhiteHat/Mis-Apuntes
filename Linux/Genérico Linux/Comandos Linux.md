
| Comando        | Descripción                                                                                                                                                                                                  |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Head**       | Permite ver las 10 primeras lineas de un texto                                                                                                                                                               |
| **Tail**       | Permite ver las 10 primeras lineas de un archivo                                                                                                                                                             |
| **Diff**       | Compara dos contenidos de un archivo línea por línea. Tras analizarlos, mostrará las partes que no coincidan.                                                                                                |
| **Find**       | Buscar archivos dentro del directorio                                                                                                                                                                        |
| **Grep**       | Encontrar palabras                                                                                                                                                                                           |
| **Locate**     | Encontrar archivos en sistema (-i desactiva mayusculas y minusculas)                                                                                                                                         |
| **Df**         | Informa sobre el uso del espacio en disco del sistema, mostrado en porcentaje y en kilobytes                                                                                                                 |
| **Du**         | Comprobar cuánto espacio ocupa un archivo o un directorio                                                                                                                                                    |
| **Touch**      | Crear archivo vacio                                                                                                                                                                                          |
| **Chown**      | Permite cambiar la propiedad de un archivo, directorio o enlace simbólico a un nombre de usuario específico                                                                                                  |
| **Jobs**       | Mostrar todos los procesos en ejecución                                                                                                                                                                      |
| **History**    | Muestra el historial de comandos utilizados desde que se inicio el sistema                                                                                                                                   |
| **Alias**      | Crear acceso directo                                                                                                                                                                                         |
| **Htop**       | Monitoriza recursos del sistema                                                                                                                                                                              |
| **Whatis**     | Muestra información de un comando                                                                                                                                                                            |
| **!$**         | Añade el contenido del ultimo comando                                                                                                                                                                        |
| **echo $0**    | Muestra la shell actual                                                                                                                                                                                      |
| **TTY**        | Muestra la shell actual de otra forma                                                                                                                                                                        |
| **File**       | Muestra el tipo de archivo                                                                                                                                                                                   |
| **Watch**      | Este comando se utiliza para ejecutar repetidamente otro comando con un intervalo de tiempo especificado y mostrar la salida en la consola. Es útil para monitorear cambios o actualizaciones en tiempo real |
| **tee**        | Con este comando mostrara el contenido del archivo a la vez que nos lo guarda en otro fichero                                                                                                                |
| **sshconvert** | Convierte un archivos xlsx a csv                                                                                                                                                                             |
| **xargs**      | Se utiliza para construir y ejecutar líneas de comando a partir de la salida de otros comandos o de archivos                                                                                                 |
| **wc -w**      | Contar numero de palabras de un archivo                                                                                                                                                                      |
| **less/more**  | Permiten desplazarte hacia arriba y hacia abajo en la salida del comando                                                                                                                                     |
| **Which**      | Busca en el path si el comando esta disponible y donde esta ubicado                                                                                                                                          |
|                |                                                                                                                                                                                                              |


![[Pasted image 20240620082311.png]]

# **Gestores de paquetes**
```
apt
apt-get
yum
dnf
zypper
```


# **Ocultar prueba pentesting**
```
kali-undercover
```

# Cambiar shell
```
chsh -s /bin/bash
```

# Comandos hacking
## **Abrir terminal linux**
```Bash
script /dev/null -c bash
```

## **Encontrar binarios**
```Bash
find / -perm -4000 2>/dev/null
```

## **Encodear base64**
```bash
echo 'IWQwbnRLbjB3bVlwQHNzdzByZA==' | base64 -d 
```

## **Revisar puertos internos**
```Bash
netstat -tplug
```

## **Abrir terminal con Python**
```Bash
python3 -c 'import pty; pty.spawn("/bin/sh")'
```

## **Generar clave SSH**
```Bash
ssh-keygen -f id_rsa
```

# Descodificar base 64
```Bash
base64 -d fichero.txt
```

# Añadir contenido con echo sin sobrescribir
```Bash
echo "10.10.11.177 redrules.thm" | sudo tee -a /etc/hosts
```

# Curl
```Bash
curl -i -X OPTIONS http://cyberlens.thm
````

# Crear interfaz de red
```
sudo ip tuntap add user $USER mode tun ligolo
```

# Eliminar interfaz de red
```
sudo ip link delete ligolo
```

# Añadir ruta red
```
sudo ip route add 10.10.10.0/24 dev ligolo
```

# Convertir archivo xlsx a csv
```
sudo ssconvert employee_status.xlsx employee.csv
```

# Entorno virtual con Python
## **Instalar entorno virtual**
```Bash
sudo apt install python3.11-venv #Instala una version concreta desde python
```

## **Crear entorno virtual Python**
```
python3 -m venv venv
source venv/bin/activate
```

## **Activar entorno virtual**
```
source /opt/impacket/venv/bin/activate
```
![[Pasted image 20240716134137.png]]

## **Desactivar entorno virtual**
Como podemos ver con el siguiente comando lo desactivamos y si revisamos a la derecha desaparece el entorno virtual de impacket
```
deactivate
```
![[Pasted image 20240716134200.png]]


# Entorno virtual con Pip
## **Instalar virtualenv**
```Bash
pip install virtualenv #Instala desde pip
```

## **Crear entorno virtual**
```
virtualenv proyecto_entorno
```

## **Activar entorno virtual**
```
source proyecto_entorno/bin/activate
```

# ARP
```
arp -a
route -n
ip route
```

# DNS
Añadiremos en el archivo `/etc/resolv.conf` la ip de la maquina
![[Pasted image 20240718091607.png]]

Y ahora podemos usar nslookup y dig para verificar si ya esta resuelto el problema de la resolucion de DNS
```
nslookup -type=SRV _ldap._tcp.spookysec.local 10.10.193.144
```
![[Pasted image 20240718091654.png]]

Y con dig
```
dig @10.10.193.144 _ldap._tcp.spookysec.local SRV
```
![[Pasted image 20240718091737.png]]
- `_ldap._tcp.spookysec.local`: Esto es el nombre del servicio y el dominio para el cual estamos solicitando información de registro de tipo SRV. En DNS, los registros SRV (Service) se utilizan para especificar el nombre de dominio y el puerto de los servicios ofrecidos por una máquina.
Para entender mejor por qué se añade `_ldap._tcp.spookysec.local SRV`, hay que entender el significado de cada parte:
- `_ldap`: Es el nombre del servicio que estamos buscando. En este caso, `_ldap` se refiere a Lightweight Directory Access Protocol, utilizado comúnmente en sistemas de directorios como Active Directory de Microsoft.
- `_tcp`: Indica el protocolo utilizado, en este caso, TCP (Transmission Control Protocol).
- `spookysec.local`: Es el nombre del dominio donde se está buscando el registro SRV.

# Privilegios
- `sudo -l`: Conoce los comandos que puedes ejecutar con root o otro usuario
- `sudo -V`: Ver version de sudo

# Crear hash desde comando el linux
```
openssl passwd -1 -salt abc password
```

- **openssl passwd**: Este es el comando principal de OpenSSL utilizado para generar contraseñas hash.
- **-1**: Esto especifica el tipo de algoritmo de hash a utilizar. En este caso, "-1" indica el uso del algoritmo de hash MD5.
- **-salt abc**: Esto establece un valor de salto específico. El salto es una cadena aleatoria que se concatena a la contraseña antes de generar el hash, lo que aumenta la seguridad del hash.
- **password**: Esta es la contraseña para la cual se generará el hash.

Entonces, el comando genera un hash de contraseña utilizando el algoritmo de hash MD5, con un salto específico "abc", para la contraseña proporcionada "password". El resultado es un hash de contraseña que puede ser almacenado y utilizado para autenticación.

# Información sistema
uname -m
arch
![[Pasted image 20240201121746.png]]

cat /etc/*release
![[Pasted image 20240429080342.png]]

# Activar zsh
Para activarlo tenemos que añadir la siguinte linea a la configuración del fichero `zshrc`
```Bash
echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> /home/wolf/.zshrc
```
![[Pasted image 20240607123244.png]]

El comando de abajo muestra cada segundo la modificación final del archivo, si quisieramos mostrar el principio cambiariamos tail por less
```bash
watch -n 1 "tail /home/wolf/.zshrc"
```


# Generar sesión interactiva en Linux
```
bin/bash -i
```

```
bin/sh
```

```
python -c 'import pty; pty.spawn("/bin/bash")'
```

# Diff
Diff es una utilidad para la comparación de archivos que genera las diferencias entre dos archivos o los cambios realizados en un archivo determinado comparándolo con una versión anterior del mismo archivo. Diff expone los cambios realizados por línea en los archivos de texto.

Ejemplo de uso para comparar archivos
```
diff -u archivo1.sh archivo2.sh > parche.patch
```

# Patch
Patch es un **comando de Unix y Unix-like que actualiza ficheros de texto de acuerdo a las instrucciones contenidas en un archivo separado, llamado archivo de parche**.
```
patch archivo 1.2 < parche.patch
```

## Abrir y comparar dos archivos
```
vimdiff archivo1 archivo2
```

# Discos y  Particiones
## **Comandos discos duros**
```
lsblk -fm
fdisk -l
lsscsi
df -h
```
![[Pasted image 20240215074559.png]]
![[Pasted image 20240215074720.png]]
![[Pasted image 20240215074748.png]]

## **Desmontar disco y formatear**
```
umount /dev/vdb
```
![[Pasted image 20240215081926.png]]
![[Pasted image 20240215085050.png]]
En este caso aparecen dos pero con el comando echo previamente apareceria uno unicamente, esto es debido a que he creado particiones con pruebas realizadas mas abajo.

## **Montar disco**
```
mkdir -p /mnt/disco_extra
mount /dev/vdb /mnt/disco_extra
df -h
```
![[Pasted image 20240215081530.png]]

### **Verificar procesos disco**
```
lsof /dev/vdb
```
![[Pasted image 20240215080441.png]]

Matamos los procesos
![[Pasted image 20240215080553.png]]

## **Verificar sistema de archivos**
```
file pspy64
```
[[Pasted image 20240215082102.png]]
![[Pasted image 20240712094756.png]]

## **Verificar el UUID del sistema de archivos**
```
blkid /dev/vdb
```
![[Pasted image 20240215082143.png]]

## **Acceder al disco**
```
cd /mnt/disco_extra
```
![[Pasted image 20240215082513.png]]

## **Crear particiones con fdisk**
fdisk /dev/vdb
- d: Eliminar particiones
- w: Escribir cambios en el disco
- o: Crear tabla de particiones
- n: Crear nueva particion
	- p: Primaria
	- e: Extendida
![[Pasted image 20240215075344.png|500]]

## **Crear particiones con gdisk**
Seleccionar disco
![[Pasted image 20240215095023.png]]


## **Gestionar particiones con gparted**
![[Pasted image 20240215095236.png]]
## **Permisos archivos y directorios**
ls -l /dev/vdb1
![[Pasted image 20240215113741.png]]

## **Verificar errores de hardware**
fsck /dev/vdb1

Registros del sistema
```
journalctl
```
![[Pasted image 20240704140322.png]]

# Alias
Un alias es un atajo o nombre alternativo que puedes asignar a un comando o a una serie de comandos. Esto te permite ejecutar comandos largos o complicados con una palabra más corta y fácil de recordar.

Creamos el alias
![[Pasted image 20240708081408.png]]

Verificamos que esta configurado
![[Pasted image 20240708081458.png]]

Y al ejecutarlo realizara la acción configurada
![[Pasted image 20240708081527.png]]


# Actualizar locate
```
sudo updatedb
```
![[Pasted image 20240717103702.png]]

# Comando Xargs
Es muy útil para trabajar con grandes cantidades de datos, permitiendo procesar múltiples elementos a la vez o en grupos, y pasar la salida de un comando como argumentos para otro de una manera flexible.

## **Eliminar archivos listados con find**
Este comando busca todos los archivos con extensión `.log` en `/ruta` y luego usa `xargs` para pasarlos como argumentos al comando `rm`, eliminándolos.
```
find /ruta -name "*.log" | xargs rm
```

## **Contar palabras en multiples archivos**
Este comando toma todos los archivos `.txt` en el directorio actual, y los pasa como entrada al comando `wc -w` para contar las palabras.
```
ls *.txt | xargs wc -w
```

## **Limitar el numero de argumentos por línea**
Este comando encuentra todos los archivos `.jpg` en `/ruta` y copia 10 archivos a la vez al directorio `/destino`.
```
find /ruta -name "*.jpg" | xargs -n 10 cp -t /destino
```

## **Usar Xargs con entrada estandar**
Esto crearía tres archivos llamados `archivo1`, `archivo2` y `archivo3`.
```
echo "archivo1 archivo2 archivo3" | xargs touch
```

# Comando init
**init** es un comando que interactúa con el **sistema de inicio** y **gestor de niveles de ejecución** (runlevels) en Unix/Linux. El sistema de inicio controla el estado del sistema, como el apagado, el reinicio, o los diferentes modos de operación (ejemplo: modo de usuario único o multiusuario).
• **0**: Apagado del sistema.
• **1**: Modo de usuario único.
• **3**: Modo multiusuario sin interfaz gráfica.
• **5**: Modo multiusuario con interfaz gráfica.
• **6**: Reiniciar el sistema.

Alernatvias comando init:
• **reboot** — para reiniciar el sistema.
• **shutdown -r now** — para reiniciar el sistema inmediatamente.


# **Cambiar teclado español temporal**
```
sudo loadkeys es
```