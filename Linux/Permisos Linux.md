Los permisos en sistemas Linux son fundamentales para la seguridad y la gestión de archivos y directorios. Se dividen en tres categorías principales: lectura (r), escritura (w) y ejecución (x), y se aplican a tres tipos de usuarios: propietario (owner), grupo (group) y otros (others). Estos permisos se representan en forma de cadenas de caracteres en la salida del comando `ls -l`, por ejemplo, "rw-r--r--", que indica que el propietario tiene permisos de lectura y escritura, mientras que los usuarios del grupo y otros solo tienen permiso de lectura.

# Chown
Se utiliza para cambiar el propietario y/o grupo de un archivo o directorio. El nombre "chown" proviene de las palabras "change owner", que reflejan su función principal: cambiar el propietario de un archivo o directorio.

El comando `chown` se utiliza con diferentes sintaxis para cambiar el propietario y/o grupo de un archivo o directorio. Puede ser utilizado con nombres de usuario y grupos, así como con identificadores numéricos de usuario y grupo (UID y GID).

- `chown usuario archivo`: Cambia el propietario del archivo al usuario especificado.
- `chown :grupo archivo`: Cambia el grupo del archivo al grupo especificado.
- `chown usuario:grupo archivo`: Cambia tanto el propietario como el grupo del archivo.
- `chown -R usuario:grupo directorio`: Cambia recursivamente el propietario y el grupo de un directorio y de todos los archivos y subdirectorios dentro de él.

# Ejemplos
En este comando estamos especificando permisos de lectura y escritura para el usuario root, en el primero comando indicamos quien sera el propietario y en el segundo le damos los permisos
![[Pasted image 20240314101839.png]]




# CHMOD
Se utiliza para cambiar los permisos de archivos y directorios. El nombre "chmod" proviene de las palabras "change mode", que reflejan su función principal: modificar el modo de acceso a un archivo o directorio.

Los permisos de archivo en sistemas Unix y Linux se dividen en tres categorías de usuarios: el propietario del archivo (owner), el grupo al que pertenece el archivo (group) y todos los demás usuarios (others). Para cada una de estas categorías, se pueden especificar tres tipos de permisos: lectura (read), escritura (write) y ejecución (execute).

Los permisos contienen 9 caracteres, los 3 primeros son las ver los permisos que tiene el propietario del archivo, los siguientes 3 para ver los permisos que tienen los archivos pertenecientes al grupo y los ultimos 3 digitos para comprobar los permisos del resto de usuarios

Para asignar los permisos podemos ejecutar el siguiente comando:
sudo chmod 600 archivo_ejemplo.txt
En este caso estamos indicando que el archivo tenga permisos de lectura y escritura para el usuario root, para modificar los permisos tenemos que entender que funcionan de la siguiente manera: 

- `4`: Lectura (read)
- `2`: Escritura (write)
- `1`: Ejecución (execute)

Como hemos seleccionado 600 estamos indicando que el propietario tiene permisos de lectura y escritura 4+2=6 y el resto de usuarios no tienen acceso

## **Comandos CHMOD**
- `chmod +x archivo`: Agrega el permiso de ejecución al archivo para todos los usuarios.
- `chmod u+x archivo`: Agrega el permiso de ejecución al propietario del archivo.
- `chmod go-r archivo`: Elimina el permiso de lectura para el grupo y otros usuarios.

### **Dar permisos**
chmod 755 archivo.txt
![[Pasted image 20240314104052.png]]

### **Agregar permisos de ejecución**
chmod +x archivo.txt
![[Pasted image 20240314103556.png]]


## **Permisos especiales**
### **Permisos SETGID**
  
El permiso setgid (Set Group ID) es un atributo especial que se puede aplicar a archivos y directorios en sistemas operativos Unix y Unix-like, como Linux. Cuando un archivo o directorio tiene el permiso setgid activado, los nuevos archivos creados dentro de ese directorio heredan automáticamente el grupo del directorio en lugar del grupo primario del usuario que los creó.

Para archivos ejecutables, el setgid funciona de manera similar al setuid, pero en lugar de ejecutarse con los privilegios del propietario del archivo, se ejecutan con los privilegios del grupo al que pertenece el archivo.

El permiso setgid se representa en la salida del comando `ls -l` como una 's' en lugar de una 'x' en el lugar de los permisos de ejecución para el grupo. Por ejemplo, si un directorio tiene permisos `rwxrwsr-x`, significa que el bit setgid está activado en el directorio.

El permiso setgid es útil en situaciones donde múltiples usuarios necesitan trabajar en un conjunto común de archivos y se necesita garantizar que los nuevos archivos creados hereden adecuadamente los permisos del grupo. Sin embargo, su uso también debe ser cuidadosamente considerado para evitar posibles problemas de seguridad.
Permite que todos los archivos que se crean dentro del directorio pertenezan al mismo grupo que el directorio, en lugar de tener los permisos del usuario que los crea
sudo chmod g+s carpeta

### **Permisos SETUID**
El permiso setuid (Set User ID) es un atributo especial que se puede aplicar a archivos ejecutables en sistemas basados en Unix y Unix-like, como Linux. Cuando un archivo tiene el permiso setuid activado, se ejecuta con los permisos del propietario del archivo en lugar de los permisos del usuario que lo está ejecutando. Esto significa que cuando un usuario ejecuta un archivo con el permiso setuid activado, el programa se ejecuta con los mismos privilegios que el propietario del archivo, generalmente el usuario root.

El permiso setuid se representa en la salida del comando `ls -l` como una 's' en lugar de la 'x' en el lugar de los permisos de ejecución para el propietario del archivo. Por ejemplo, si un archivo tiene permisos `rwsr-xr-x`, significa que el bit setuid está activado.

![[Pasted image 20240314135020.png]]

### **Permisos**
#### **Dar permisos al servicio postgresql**
```
usermod -aG postgres root
```
![[Pasted image 20240304090027.png]]

#### **Eliminar permisos al servicio postgresql**
```
gpasswd -d root postgres
```
![[Pasted image 20240304090131.png]]


# SETFACL
El comando `setfacl` se utiliza en sistemas Unix y Unix-like para establecer los Controles de Acceso de Lista de Control (ACL, por sus siglas en inglés) en archivos y directorios. Los ACL permiten un control más granular sobre los permisos de acceso a archivos y directorios en comparación con los permisos de usuario/grupo estándar (propiedad del sistema de archivos).

Los permisos de usuario/grupo tradicionales (como los mostrados por el comando `ls -l`) se limitan a propietario, grupo y otros usuarios. Sin embargo, los ACL permiten asignar permisos específicos a usuarios individuales y a grupos, lo que proporciona un mayor nivel de control sobre quién puede acceder y qué operaciones pueden realizar en los archivos y directorios.

El comando `setfacl` se utiliza para establecer estos ACL. Permite agregar, modificar o eliminar entradas de ACL en archivos y directorios, definiendo permisos específicos para usuarios y grupos.

Por ejemplo, con `setfacl`, puedes otorgar a un usuario específico permisos de lectura y escritura en un archivo, incluso si no es el propietario del archivo ni pertenece al grupo propietario.

El uso detallado del comando `setfacl` varía según el sistema operativo y la distribución Linux específica. Puedes consultar la documentación o ejecutar `man setfacl` en tu sistema para obtener más información sobre cómo usar este comando en tu entorno específico.