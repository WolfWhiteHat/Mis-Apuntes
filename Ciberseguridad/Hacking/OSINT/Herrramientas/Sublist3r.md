### Que es Sublist3r
Sublist3r **es una herramienta de Python diseñada para enumerar subdominios de sitios web que usan OSINT**. Ayuda a los probadores de penetración y cazadores de errores a recopilar y recopilar subdominios para el dominio al que se dirigen.

Para instalar sublim3r utilizaremos el siguiente comando
apt-get install sublist3r
![[Pasted image 20240313103403.png]]


Para realizar una busqueda de subdominios de una URL escribiremos el siguiente comandp
sublist3r -d hackersploit.org -e google,yahoo
la opción -d es para indicar el dominio, con el comando -e especificamos los motores de busqueda
![[Pasted image 20240313103443.png]]

Como podremos ver en la siguiente imagen utiliza todas las herramientas y en este caso si que nos ha encontrado subdominios
![[Pasted image 20240313104505.png]]