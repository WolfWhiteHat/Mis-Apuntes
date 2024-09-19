En Metasploit, hay dos formas principales de interactuar con las bases de datos: utilizando el comando `db_` o utilizando el servicio `msfdb`.

1. **`db_` Commands**:
    - `db_` commands son aquellos que se usan para interactuar directamente con la base de datos de Metasploit.
    - Estos comandos permiten gestionar hosts, servicios, vulnerabilidades, exploits y sesiones dentro de la base de datos.
    - Por ejemplo, puedes usar comandos como `db_nmap` para importar resultados de escaneos de Nmap a la base de datos, o `db_autopwn` para seleccionar y ejecutar exploits automáticamente contra objetivos.
    - Estos comandos son útiles para tareas de análisis y gestión de datos almacenados en la base de datos de Metasploit.
2. **`msfdb` Service**:
    - `msfdb` es un servicio que se utiliza para gestionar la base de datos de Metasploit.
    - Este servicio proporciona funcionalidades para iniciar, detener, reiniciar, y administrar la base de datos de Metasploit.
    - Con `msfdb`, puedes iniciar o detener el servicio de base de datos, inicializar o migrar la base de datos, y administrar usuarios y roles de la base de datos.
    - Esencialmente, `msfdb` es una herramienta para administrar la base de datos de Metasploit como un servicio separado.

En resumen, mientras que los comandos `db_` son utilizados para interactuar directamente con la base de datos dentro de Metasploit, `msfdb` es utilizado para gestionar el servicio de base de datos en sí mismo, incluyendo su inicio, detención y gestión de usuarios. Dependiendo de la tarea que estés realizando, puedes necesitar usar uno u otro, o incluso ambos en conjunto.

### Arrancar postgresql
Para poder utilizar la BBDD de metasploit primero tendremos que arrancar en nuestro sistema postgresql, sin ello no podremos crear BBDD dentro de metasploit
#### Postgresql
sudo systemctl enable postgresql
sudo systemctl start postgresql
sudo systemctl status postgresql

## Crear docuemento para importar
Para importar un documentos a metasploit primero necesitaremos crearlo
nmap -sV -O 10.2.24.223 -oX Escaneo
![[Pasted image 20240320082458.png]]

### Arrancar servicio
Arrancamos el servicio de BBDD y ejecutamos metasploit
service postgresql start && msfconsole
![[Pasted image 20240320082553.png]]

### Comandos BBDD

##### Interactuar con MSFDB
Para interactuar con la base de datos de metasploit utilizaremos el siguiente comando
sudo msfdb
![[Pasted image 20240318114438.png]]

## Comprobar estado BBDD Metasploit
Con el siguiente comando comprobamos el estado de la base de datos dentro de metasploit
db_status
![[Pasted image 20240320083047.png]]


## Importar documento
db_import Escaneo
![[Pasted image 20240320085024.png]]

# Comandos Base de datos Metasploit
- `hosts`: Este comando muestra una lista de los hosts identificados dentro del proceso actual de escaneo o explotación en Metasploit. Proporciona información sobre las direcciones IP, nombres de host y otros detalles relevantes de los hosts objetivo.

- `services`: Al ejecutar este comando, se muestran los servicios activos detectados en los hosts objetivo. Proporciona información sobre los puertos abiertos, los servicios asociados a dichos puertos y otra información útil relacionada con los servicios en los hosts.

- `vulns`: El comando `vulns` muestra una lista de las vulnerabilidades identificadas en los hosts objetivo durante el escaneo y la exploración en Metasploit. Proporciona detalles sobre las vulnerabilidades específicas encontradas, sus categorías y gravedad.

- `loot`: Al utilizar el comando `loot`, se accede a la información recolectada y cualquier dato importante que ha sido obtenido durante el proceso de explotación. Esto puede incluir credenciales, archivos, datos confidenciales u otro tipo de información valiosa.

- `creds`: El comando `creds` muestra las credenciales recuperadas o descubiertas durante las actividades de escaneo y explotación en Metasploit. Proporciona información sobre nombres de usuario, contraseñas u otros datos de autenticación comprometidos.

- `notes`: Al ejecutar el comando `notes`, se muestran las notas o comentarios agregados por el operador durante el proceso de trabajo en Metasploit. Estas notas pueden contener información importante, observaciones o acciones a realizar en un momento posterior.

- `sessions`: Este comando muestra una lista de las sesiones de Metasploit que han sido establecidas con dispositivos remotos vulnerables. Proporciona detalles sobre las sesiones activas, incluidos los ID de sesión, los hosts conectados y el tipo de sesión abierta.




