Autopsy es un software libre y de código abierto para análisis forense digital. Se utiliza para examinar discos duros, imágenes de discos y otros dispositivos de almacenamiento en busca de evidencia digital. Autopsy puede utilizarse para recuperar archivos eliminados, analizar registros de eventos y rastrear la actividad del usuario.

Autopsy es una herramienta muy potente que puede utilizarse para una variedad de propósitos, incluyendo:

- Investigaciones criminales
- Investigaciones corporativas
- Investigaciones de seguridad informática
- Análisis de malware
- Recuperación de datos

Autopsy es una herramienta muy fácil de usar. Tiene una interfaz gráfica de usuario (GUI) intuitiva que facilita la navegación y el uso de las diferentes funciones del software. Autopsy también está disponible en una versión de línea de comandos para usuarios más avanzados.

### Tutorial Autopsy

Lo primero que tendremos que hacer es una busqueda de los discos y ver cual queremos analizar, en nuestro caso hemos creado un disco vdb, crearemos un fichero y lo borraremos por completo del sistema
![[Pasted image 20240215074112.png]]

Como podemos ver en la siguiente imagen hemos creado un fichero y lo vamos a eliminar
![[Pasted image 20240215115913.png|500]]

Con el siguiente comando realizaremos una imagen del disco para posteriormente analizarla con la herramienta de Autopsy
dd if=/dev/vdb of=/home/wolf/Escritorio/test_autopsy.iso
![[Pasted image 20240215120416.png]]

Arrancamos la herramienta con el comando
autopsy
![[Pasted image 20240215120540.png]]

Copiamos la url de abajo y la pegamos en el navegador
http://localhost:9999/autopsy
![[Pasted image 20240215120704.png]]
Accedemos a new case

Creamos el caso
![[Pasted image 20240215120852.png]]

Creamos el host
![[Pasted image 20240215120930.png|400]]
![[Pasted image 20240215120956.png|400]]

Añadimos la imagen
![[Pasted image 20240215121035.png|500]]

Seleccionamos add image file
![[Pasted image 20240215121108.png]]

Indicamos donde esta ubicada la imagen previamente creada del disco a examinar
![[Pasted image 20240215121755.png|500]]

![[Pasted image 20240215121926.png]]

![[Pasted image 20240215122014.png]]

![[Pasted image 20240215122037.png]]

Una vez esta creada la imagen ya podremos analizarla
![[Pasted image 20240215122110.png]]

Seleccionamos file analysis
![[Pasted image 20240215122145.png]]


Ya podríamos analizar el disco
![[Pasted image 20240215122505.png]]
