Nessus es una herramienta de escaneo de vulnerabilidades que se utiliza para identificar debilidades de seguridad en sistemas informáticos. Es una herramienta muy popular y ampliamente utilizada por profesionales de la seguridad informática.

Nessus funciona escaneando un sistema objetivo y buscando vulnerabilidades conocidas. Una vez que se encuentran las vulnerabilidades, Nessus proporciona información detallada sobre ellas, incluyendo el nivel de gravedad y las posibles soluciones.

### Tutorial Nessus
Primero instalamos nessus, para ello iremos al siguiente enlace y nos descargaremos el archivo de la ultima versión
https://docs.tenable.com/nessus/Content/InstallNessusLinux.htm#To-install-Nessus-on-Linux:

Nos descargaremos el paquete y ejecutaremos el siguiente comando
dpkg -i Nessus-10.6.4-ubuntu_aarch64.deb
![[Pasted image 20240201122050.png]]

Ahora tendremos que activar el servicio
/bin/systemetl start nessusd. service
![[Pasted image 20240201122453.png]]

Ahora ya tendremos activado el servicio de Nessus, ahora iremos al navegador y escribiremos
https://localhost:8834

Como podemos ver ya estamos dentro de Nessus, ahora vamos a crear una cuenta y registrarnos
![[Pasted image 20240201122852.png]]

Como estamos usando Nessus a nivel educativo crearemos una cuenta Essencial
![[Pasted image 20240201122943.png|300]]

Una vez registrados y activado el codigo crearemos el usuario
wolf
1234

Y ya estaremos iniciando Nessus
![[Pasted image 20240201123358.png|300]]


### Escaneo sencillo Nessus
Este es el menu principal
![[Pasted image 20240201125301.png]]
Aquí podemos escanear cualquier ip y buscara las vulnerabilidades y me las clasificara, a diferencia de nmap nos dara mas información de las vulnerabilidades, comenzaremos dandole a new scan

Como se podra ver en la siguiente imagen, Nessus tiene muchisimas herramientas, comenzaremos usando dos
![[Pasted image 20240201125437.png]]
Primero utilizaremos la primera que pone host discovery

Dentro de la configruación pondremos un titulo al escaneo y daremos la ip a escanear
![[Pasted image 20240201130912.png]]

![[Pasted image 20240201131044.png]]
Aqui ya tendremos el escaneo preparado, ahora solo faltara ejecutarlom para ello le daremos al boton del play de la derecha.

En la siguiente imagen tenemos el escaner con las vulnerabilidades
![[Pasted image 20240202114736.png]]


### Escaneo completo Nessus
![[Pasted image 20240205073910.png]]
Dentro de las opciones que tenemos para realizar un escaneo vamos a seleccionar advanced scan para encontrar todas las vulnerabilidades

Aquí tenemos la configuración que vamos a dejar
![[Pasted image 20240205074148.png]]

En la pestaña de pluggins podemos ver todos los pluggins que se utilizaran para analizar la maquina victima
![[Pasted image 20240205074222.png]]

Mientras se esta ejecutando el escaner podemos ir revisando los resultado
![[Pasted image 20240205074721.png]]
Accedemos al nuevo escaneo

Como podemos ver es un escaneo mas completo donde podremos ver mas información, en esta captura podemos comprobar que aun esta ejecutando el escaner pero nosotros podemos ir analizandolo
![[Pasted image 20240205074744.png]]

Si vamos a la pestaña de vulnerabilidades podremos ver todo lo que nos ha encontrado el escaner con su sev de seguridad
![[Pasted image 20240205074933.png]]