
![[Pasted image 20240118083617.png]]

**docker run:** crea y ejecuta un contenedor.
**docker start:** inicia un contenedor detenido.
**docker stop:** detiene un contenedor en ejecución.
**docker rm:** elimina un contenedor.
**docker pull:** descarga una imagen de contenedor del registro de Docker.
**docker push: **carga una imagen de contenedor al registro de Docker.

# Ejemplos comandos docker

Creamos y descargamos la imagen, si añadimos docker run postgres:tag, el tag es la versión que queremos descargar
![[Pasted image 20240118084117.png]]
![[Pasted image 20240118084404.png]]

Descarga la ultima imagen de ubuntu pero a diferencia de run, no corre la imagen
![[Pasted image 20240118084812.png]]

Revisamos las imagenes que tenemos
![[Pasted image 20240118085017.png]]

Muestra las imagenes descargadas
![[Pasted image 20240118085102.png]]

Muestra la ultima información de los contenedores, en este caso lo acabamos de parar y así nos lo esta especificando
![[Pasted image 20240118085428.png]]

Aquí estamos volviendo a iniciar el contendor que habíamos cerrado, para ello utilizamos docker start y la ID del contenedor
![[Pasted image 20240118085630.png]]

Con el comando docker log y el nombre o ID del contenedor vemos los logs, si hacemos docker logs -f va a seguir el log, lo vamos a poder ver en tiempo real
![[Pasted image 20240118085843.png]]

Con el siguiente comando docker exec coge un contenedor que esta iniciado a diferencia de docker run que lo crea, en este caso vemos que hemos ejecutado sh, un comando shell, con menos -i crea una sesion interactiva y -t crea un terminal
![[Pasted image 20240118090144.png]]

Con docker stop paramos el contenedor
![[Pasted image 20240118090403.png]]

Correr un contenedor en background
![[Pasted image 20240118090513.png]]

![[Pasted image 20240118090644.png]]

# Dockerfile
Fichero dockerfile
![[Pasted image 20240118092621.png]]

Construimos el contenedor y generamos una imagen con docker build
![[Pasted image 20240118092825.png]]

Aquí ya veremos la imagen construida, ahora la crearemos y ejecutaremos
![[Pasted image 20240118093406.png]]

# Puertos en docker
![[Pasted image 20240118094012.png]]

# Bibliografia
https://geekflare.com/es/docker-commands/
https://atareao.es/tutorial/docker/gestionar-contenedores-con-docker/
https://docs.docker.com/get-started/overview/
https://docs.docker.com/desktop/install/mac-install/