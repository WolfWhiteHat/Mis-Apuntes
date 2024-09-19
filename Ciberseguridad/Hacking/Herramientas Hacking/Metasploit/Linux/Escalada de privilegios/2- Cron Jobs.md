
Vamos a hacer una escalada de privilegios en linux, para ello tenemos una maquina virtual en la cual ya tenemos el acceso a la maquina victima

Primero miramos el archivo que tenemos y como podemos ver no tenemos permisos ya que solo puedo leer los fichero el usuario root
![[Pasted image 20240314125857.png]]

Hacemos una busqueda del fichero y vemos que tanto el usuario student como la carpeta /tmp se esta ejecutando una tarea que sobreescribe el archivo message cada minuto
![[Pasted image 20240314130145.png]]
![[Pasted image 20240314130427.png]]

Este comando está utilizando el programa `grep`, que se utiliza para buscar patrones de texto en archivos. Aquí está desglosado:
- `grep`: El comando de búsqueda de texto en Linux.
- `-n`: Muestra el número de línea donde se encuentra el resultado.
- `-r`: Realiza una búsqueda recursiva en directorios y subdirectorios.
- `-i`: Realiza una búsqueda que no distingue entre mayúsculas y minúsculas.
- `"/tmp/message"`: Es el patrón de búsqueda que se está utilizando.
- `/usr`: Es el directorio en el que se está buscando. En este caso, se está buscando en todo el directorio `/usr`.
La salida del comando muestra las líneas que contienen el patrón de búsqueda "/tmp/message" en los archivos dentro del directorio `/usr`. En este caso, muestra dos líneas que contienen la referencia a "/tmp/message" en los archivos `/usr/local/share/copy.sh`, junto con el número de línea en cada caso.
![[Pasted image 20240314130513.png]]

Ahora revisamos los permisos del fichero que hemos encontrado en la ruta y leeremos que hace, en la siguiente imagen podemos ver como nos a mostrado el mismo contenido que en el anterior comando
![[Pasted image 20240314130948.png]]

Ahora buscaremos añadir contenido a este fichero para obtener un usuario con privilegios, como vemos no tenemos acceso a ninguna herramienta para modificar el archivo, así que utilizaremos el siguiente comando
printf '#! /bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /usr/local/share/copy.sh
![[Pasted image 20240314131412.png]]

Si ahora leemos el fichero podemos ver que ya hemos modificado el contenido
![[Pasted image 20240314131511.png]]

Como podemos ver en el siguiente comando hemos obtenido los permisos del usuario root
sudo -l
![[Pasted image 20240314131539.png]]

Como se puede ver en la ultima imagen hemos podido acceder al usuario root
![[Pasted image 20240314132829.png]]

![[Cron Jobs.pdf]]