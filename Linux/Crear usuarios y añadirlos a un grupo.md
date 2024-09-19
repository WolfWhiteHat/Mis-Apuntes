https://www.zeppelinux.es/crear-usuarios-en-linux-desde-la-linea-de-comandos/
useradd / adduser--> Crear usuarios:
Los valores por defecto que tomará `useradd`, se configuran en el archivo `/etc/default/useradd`.

sudo adduser eric
sudo passwd eric
cat /etc/passwd | grep (user)
cat /etc/group | grep (user)
Copiar esqueleto de directorios:
sudo cp -r /etc/skel/* /home/eric
sudo mkdir -m 750 /home/eric
sudo chown mortadelo:mortadelo /home/eric/
# Crear usuario con /home
En el siguiente comando utilizaremos la opción **-m**. Creará un usuario llamado eric, le asignará la shell por defecto que en **Debian** es `/bin/sh`, le asignará y **creará** el directorio de inicio `/home/filemon`, se copian los directorios y archivos contenidos en el skeleton directory, crea el grupo eric y lo asigna al mismo y **no tiene contraseña**.

sudo useradd -m eric
sudo passwd eric

Cuando utilizas el comando **useradd**, este realiza algunos cambios importantes:
- Edita los archivos **/etc/passwd**, **/etc/shadow**, **/etc/group** y **/etc/gshadow** para las cuentas recién creadas.
- Crea y rellena un directorio personal para el usuario.
- Establece los permisos y la propiedad de los archivos en el directorio personal.

1. **/etc/passwd:** Este archivo contiene información sobre los usuarios del sistema, incluidos sus nombres de usuario, UID (identificador de usuario), GID (identificador de grupo), directorios de inicio y shells.

2. **/etc/shadow:** Este archivo almacena las contraseñas encriptadas de los usuarios.

3. **/etc/group:** Contiene información sobre los grupos del sistema, incluidos los nombres de grupo y los GIDs.

4. **/home/nuevo_usuario:** Este directorio será el directorio de inicio del nuevo usuario. Aquí es donde el usuario almacenará sus archivos personales y configuraciones.

5. **/etc/skel:** Este directorio contiene archivos y carpetas que se copian en el directorio de inicio de un nuevo usuario cuando se crea. Puedes personalizar el contenido de este directorio para proporcionar una configuración inicial específica para los nuevos usuarios.

6. **/etc/login.defs:** Archivo de configuración que define configuraciones por defecto para la creación de usuarios, como la longitud mínima de la contraseña, el número máximo de días de inactividad, etc.

7. **/etc/default/useradd (o /etc/default/adduser):** Archivo de configuración que contiene configuraciones predeterminadas para el comando `useradd` o `adduser`.

8. **/etc/sudoers:** Si deseas conceder privilegios de sudo al nuevo usuario, puedes modificar este archivo. Ten en cuenta que modificar directamente este archivo puede ser arriesgado, y se recomienda usar el comando `visudo` para hacerlo de manera segura.

# Crear usuario rapido y añadirle un passwd
![[Pasted image 20240411084659.png]]

# Añadir usuario al grupo root
Primero creamos el usuario, en este caso es ftp para esconderlo de que lo encuentren
![[Pasted image 20240411092247.png]]

Aqui ya tenemos el ususario creado, ahora queremos añadirlo al grupo root para que tenga los privilegios mas altos
![[Pasted image 20240411092450.png]]

Revisamos el grupo de root y lo añadimos al usuario previamente creado
usermod -aG root ftp
![[Pasted image 20240411092600.png]]


