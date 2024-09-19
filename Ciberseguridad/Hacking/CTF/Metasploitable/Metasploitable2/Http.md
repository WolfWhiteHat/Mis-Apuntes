Vamos a buscar explotar la vulerabilidad del protocolo 80 http

Primero analizamos la versión que tiene
![[Pasted image 20240201105721.png]]

Como podemos ver tiene instalado una version de php, para revisarlo iremos al navegador y escribiremos lo siguiente:
http://192.168.60.3/phpinfo.php
![[Pasted image 20240201105844.png]]

Probamos a utilizar otro modulo de metasploit para obtener mas información
dir_listing determinará si la lista de directorios está habilitada
![[Pasted image 20240201110050.png]]

Ahora probaremos con el modulo dir_scanner que buscará directorios interesantes
![[Pasted image 20240201110325.png]]
Como podemos ver nos ha encontrado 6 directorio, vamos a seguir recopilando información

![[Pasted image 20240201110646.png]]
![[Pasted image 20240201110713.png]]

Continuamos sacando información, ahora probaremos el modulo verb_auth_bypass que busca los ficheros options y robots.txt
![[Pasted image 20240201111018.png]]

Una vez recopilada la información, vamos a realizar la busqueda de un explit para atacar la maquina, para ello realizaremos una busqueda de exploits compatibles con la versión previamente detectada
![[Pasted image 20240201111243.png]]

Ahora prepararemos el exploit, configuraremos los parametros y lo ejecutaremos
![[Pasted image 20240201111904.png]]

