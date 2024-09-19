
# Instalacion y puesta en marcha de Postgresql

Actualizamos el sistema e instalamos el servicio postgresql
![[Pasted image 20240321080219.png|1500]]

Verificamos version instalada
![[Pasted image 20240321080421.png]]

Arrancamos el servicio, como vemos un errors miramos el estado actual
![[Pasted image 20240321080516.png]]

El servicio no esta arrancado y nos indica que tiene errores, para revisarlo escribiremos el siguiente comando
journalctl -xeu postgresql.service
- `journalctl`: Es un comando que permite consultar los registros del sistema utilizando el sistema de registro journalctl de systemd en sistemas Linux modernos.
- `-xeu postgresql.service`: Son opciones del comando `journalctl`:
    - `-x`: Muestra el registro en modo de salida detallada (verbose).
    - `-e`: Salta al final del registro.
    - `-u postgresql.service`: Filtra los registros para mostrar solo los relacionados con el servicio `postgresql.service`.
![[Pasted image 20240321080559.png]]![[Pasted image 20240321080653.png]]

Buscamos el usuario postgres, al ver que no esta creado y es necesario para poder utilizar postgresql lo creamos
- `sudo adduser postgres --disabled-password --system --group`: Este comando agrega un nuevo usuario llamado "postgres" al sistema. Aquí está el significado de cada opción:
    - `--disabled-password`: Crea el usuario sin una contraseña asignada. Esto es común para cuentas de sistema que no necesitan iniciar sesión directamente.
    - `--system`: Crea un usuario del sistema. Estos son usuarios utilizados para operaciones del sistema y no deben usarse para iniciar sesión de forma interactiva.
    - `--group`: Crea un grupo con el mismo nombre que el usuario y asigna al usuario a este grupo. En este caso, se crea un grupo llamado "postgres" y el usuario "postgres" se agrega a este grupo.
![[Pasted image 20240321080718.png]]

Reinciamos el servicio y continuamos viendo que falla
![[Pasted image 20240321080915.png]]

Volvemos a ejecutar los logs, como vemos que continua teniendo fallos resintalamos el servicio
![[Pasted image 20240321081027.png|1500]]

Vuelve a fallar la ejecución del servicio, revisamos los fallos
![[Pasted image 20240321081155.png]]

El siguiente registro nos muestra el error que no encuentra el siguiente directorio
/var/lib/postgresql/15/main, asi que lo creamos y le damos los permisos al usuario postgres previamente creado
![[Pasted image 20240321081328.png]]


Volvemos a ejecutar el servicio y volvemos a ver otro fallo, en este caso el error muestra que el directorio que hemos creado antes no es un directorio de base de datos
![[Pasted image 20240321081457.png]]


Para solucionarlo ejecutaremos los siguiente comandos
1. `sudo rm -rf /var/lib/postgresql/15/main`: Este comando elimina de forma recursiva y forzada el directorio `/var/lib/postgresql/15/main`, que es el directorio de datos de PostgreSQL para la versión 15.
2. `sudo -u postgres /usr/lib/postgresql/15/bin/initdb -D /var/lib/postgresql/15/main`: Este comando inicializa un nuevo clúster de base de datos de PostgreSQL en el directorio `/var/lib/postgresql/15/main`. Aquí está el detalle de lo que hace:
    - `sudo -u postgres`: Ejecuta el comando como el usuario `postgres`.
    - `/usr/lib/postgresql/15/bin/initdb`: Es el ejecutable que inicializa el clúster de base de datos.
    - `-D /var/lib/postgresql/15/main`: Especifica el directorio donde se almacenarán los datos del clúster de base de datos.

Después de ejecutar este comando, se crean los directorios necesarios, se configura el clúster de base de datos con la codificación y la configuración regional adecuadas, y se inicializan los archivos de configuración.

Al final, el comando imprime un mensaje de éxito, indicando que el clúster de la base de datos se ha inicializado correctamente y proporciona instrucciones para iniciar el servidor de la base de datos usando `/usr/lib/postgresql/15/bin/pg_ctl`.
![[Pasted image 20240321081844.png]]

Volvemos a reinciar el servicio y como podemos ver ya funciona correctamente
![[Pasted image 20240321082001.png]]


El comando `sudo systemctl enable postgresql` está habilitando el servicio de PostgreSQL para que se inicie automáticamente en el arranque del sistema. Esto se logra creando un enlace simbólico desde el archivo de servicio de systemd `/usr/lib/systemd/system/postgresql.service` al directorio de destino `/etc/systemd/system/multi-user.target.wants/`, que es donde se almacenan los enlaces simbólicos de los servicios habilitados.
![[Pasted image 20240321082056.png]]



## Crear base de datos de Postgresql
sudo -u postgresql psql
CREATE DATABASE [nombre_BBDD]
\l verificar base de datos existentes
![[Pasted image 20240329115016.png]]

## Crear usuario y asignar roles en postgresql
CREATE ROLE usrbd WITH LOGIN PASSWORD '1234';
GRANT ALL PRIVILEGES ON DATABASE msf TO usrbd;
![[Pasted image 20240329115741.png]]