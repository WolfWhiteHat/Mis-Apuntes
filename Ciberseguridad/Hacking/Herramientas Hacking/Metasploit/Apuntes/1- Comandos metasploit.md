# Comandos Metasploit
- `msfconsole`
- `help`
- `search [vulnerabilidad]`
- `show`:  exploits, payloads, auxiliary, options
- `info`: Muestra la funciona que ejecuta el modulo seleccionado
- `set payload [opción]`
- `set RHOST [IP]`: configuras la ip que vamos a atacar
- `setg RHOSTS`: Configura por defecto una ip victima para todos los modulos de metasploit
- `set LHOST`: Seleccionamos nuestra ip
- `set [paramtetro] ""`: Dejamos el campo vacio
- `setg`: Selecciona un parametro y lo deja por defecto para todos los modulos
- `options`: Muestra las opciones de la herramienta a ejecutar
- `advance`: Muestra opciones avanzadas de options
- `run`: ejecuta el ataque
- `exploit`: ejecuta el exploit
- `back`: vuelve al inicio de la aplicación de metasploit
- `msfdb`: Servicio Base de datos de metasploit
- `db_`: Comandos BBDD
- `db_status`: Comprueba estado BBDD
- `db_namp`: Utiliza nmap desde metasploit
- `show all`: Muestra todos los modulos de metasploit
- `connect`: Similar a netcat
- `workspace`: Gestiona los espacios de trabajo
- `hosts`: Muestra los hosts a los cuales hemos intentado establecer conexión
- `vulns`: Muestra las vulnerabilidades 
- `sessions`: Muestra las sesiones activas
- `sesssions -l`: Muestra un listado de todas las sesiones
- `session -i [ID]`: Te permite interactuar con las sesiones
- `sessions -i 1`: Seleccionas la sesión con la que quieres interactuar
- `sessions -k [ID]`;: Mata la sesión seleccionada
- `sessions -K`: Matar todas las sesiones
- `background`: Te devuelve al modo de comando principal de Metasploit, saliendo de la sesión pero dejándola activa en segundo plano.
- `search type:auxiliary name:ftp`: Realiza una busqueda de todos los modulos auxiliares de ftp
- `search platform:windows`: Realiza una busqueda de modulos solo de windows
- `load db_autopwn`: Carga el pluging que hayamos añadido previamente en metasploit

Ctrl+Z Volver atras de la sesion sin cerrarla

## Comando busqueda especifica
Para realizar busquedas mas precisas sobre un modulo una vez lo hemos buscado podemos especificar mas con las siguientes opciones
```
type:auxiliary
name:ftp
platform: windows
cve:2017
```
![[Pasted image 20240321091544.png]]
## Ruta directorios Metasploit

### Wordlists
/usr/share/metasploit-framework/data/wordlists/ 

### Modulos
/usr/share/metasploit-framework/modules

### Modulos propios
~/.ms4/modules
/home/wolf/.ms4/modules

### Scripts
/usr/share/metasploit-framework/scripts/resource/

## Instalar Metasploit
sudo apt-get update && sudo apt-get install metasploit-framework -y


## Ejemplo conexión shell

Acceder a metasploit
msfconsole
![[Pasted image 20240314074243.png|500]]


Buscamos exploits
search proftpd 1.3.5
![[Pasted image 20240314074327.png]]


Seleccionamos el exploit
use 0
![[Pasted image 20240314074405.png]]

Configuramos el exploit y payload
![[Pasted image 20240314074826.png]]
![[Pasted image 20240314074811.png]]


Ejecutamos el exploit y como podemos ver ya tenemos una sesion en la maquina victima
![[Pasted image 20240314074952.png]]



## Ejemplos Metasploit
### Ver las sesiones abiertas
sessions
![[Pasted image 20240314075019.png]]


#### Conectarse a una sesion abierta
session -i [ID]
![[Pasted image 20240314075138.png]]

#### Guardar la sesion
background
![[Pasted image 20240314075225.png]]


#### Obtener sesion shell
shell
![[Pasted image 20240314075759.png]]


### Enumerar grupos
groups
![[Pasted image 20240314075946.png]]

### Enumerar usuarios del sistema
cat /etc/passwd
![[Pasted image 20240314080042.png]]

## Automatizar scripts con Metapsloit

Los script que estan creados por defecto se encuentran en la siguiente ruta
`/usr/share/metasploit-framework/scripts/resource/`

Para crear un scrip utilziaremos un editor y crearemos el scrip con el contenido que queramos ejecutar, como veremos en la siguiente imagen en un editor de texto hemos añadido los comandos que ejecutariamos en la consola de metasploit
![[Pasted image 20240325192319.png]]

Una vez creado el scrip para ejecutarlo utilziaremos el siguiente comando
`msfconsole -r handler.rc

Con el siguiente comando cargaremos el script en metasploit
`resource ~/Desktop/handler.rc`