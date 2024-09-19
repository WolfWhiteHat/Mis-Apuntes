https://howtoforge.es/como-instalar-jenkins-en-ubuntu-22-04/

Antes de empezar a instalar Jenkins necesitaremos tener instalado OpenJDK
## Instalación OpenJDK
sudo apt update
sudo apt upgrade
![[Pasted image 20231113111407.png]]

sudo apt install default-jre default-jdk
![[Pasted image 20231113111744.png]]

Comprobamos que este instalado y su versión
![[Pasted image 20231113111950.png]]

Ahora ya podemos proceder a instalar Jenkins

## Instalar Jenkins

Primero añadimos las claves GPG para los repositorios de Jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
![[Pasted image 20231113115021.png]]

Añadimos el repositorio Jenkins a nuestro sistema
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
![[Pasted image 20231113115119.png]]

Actualizamos repositorio
![[Pasted image 20231113115155.png]]

Instalamos Jenkins
sudo apt install jenkins
![[Pasted image 20231113115233.png]]

En este caso podemos ver que ya tengo instalado Jenkins

Con los siguientes comandos iniciamos y habilitamos el servicio de Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
![[Pasted image 20231113130021.png]]

Ahora verificamos que este funcionando el servicio correctamente
sudo systemctl status jenkins
![[Pasted image 20231113130322.png]]

Una vez iniciado Jenkins necesitaremos saber la contraseña para poder acceder
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
![[Pasted image 20231113131020.png]]

Por defecto Jenkins se configura en el puerto 8080
Para acceder nos vamos al navegador y escribimos lo siguiente
http://localhost:8080/
![[Pasted image 20231113131213.png]]

La contraseña la habremos sacado previamente del archivo de initialAdminPassword

Seleccionamos install suggested plugins
![[Pasted image 20231113131419.png]]

Y ya comenzara a instalarse los plugins
![[Pasted image 20231113131513.png]]

Una vez termine de instalarse configuraremos un user admin
![[Pasted image 20231113132027.png]]


Ahora configuraremos la URL de Jenkins
http://jenkinsuoc/
![[Pasted image 20231113132151.png]]

Y ya tendríamos configurado Jenkins
![[Pasted image 20231113132446.png]]


## Configuración de Jenkins para despliegue automático desde GitHub:
### Token Git Hub
Primero generamos el token de github.

Para crear un token en git hub vamos a la configuración de nuestra cuenta, a developer setting, personal acces token y nos aparecer esta pestaña
![[Pasted image 20231113185329.png]]
Aquí crearemos nuestro token, nos generara un código que posteriormente añadiremos en jenkins

Una vez tenemos el token vamos a crear una tarea en Jenkins
![[Pasted image 20231113142002.png]]

Escribimos un nombre y seleccionamos crear un proyecto de estilo libre
![[Pasted image 20231113174801.png]]



Dentro de la configuración seleccionamos el projecto de github
![[Pasted image 20231113182231.png]]

En origen de codigo fuente seleccionamos nuestro repositorio de github, también tendremos que añadir nuestras credenciales
![[Pasted image 20231113190338.png]]
![[Pasted image 20231113185203.png]]
token: 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

En disparador de ejecución selecionamos GitHub hook trigger form GITScm polling
![[Pasted image 20231113182647.png]]

## Instalar Git
Para que funcione necesitaremos instalar git en nuestro servidor
![[Pasted image 20231113182942.png]]



