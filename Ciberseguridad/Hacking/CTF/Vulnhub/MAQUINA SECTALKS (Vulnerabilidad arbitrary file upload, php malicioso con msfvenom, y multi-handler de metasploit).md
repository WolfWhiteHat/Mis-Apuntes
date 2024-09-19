Vamos a comprobar que la máquina se encuentre dentro del mismo rango de red con arp-scan:
![[Mis apuntes/ANEXOS/Pasted image 20230227123506.png]]

Y ahora haremos un escaneo de nmap y vemos que sólo tiene abierto el puerto 80:
![[Mis apuntes/ANEXOS/Pasted image 20230227123630.png]]

Podemos inspeccionar un poco más esta web antes de entrar en ella:
![[Mis apuntes/ANEXOS/Pasted image 20230227123705.png]]

Entramos a la web desde el navegador y nos encontra
![[Pasted image 20230227123745.png]]

mos con un panel de login:
![[Mis apuntes/ANEXOS/Pasted image 20230227123745.png]]

Vemos que la aplicación web se llama cutenews, por lo que miraremos si existe algún exploit con este nombre; y efectivamente existe:
![[Mis apuntes/ANEXOS/Pasted image 20230227123847.png]]

Por tanto vamos a descargarlo con el parámetro -m de searchsploit:
![[Mis apuntes/ANEXOS/Pasted image 20230227123948.png]]

Si abrimos este documento .txt veremos las instrucciones de cómo explotar esta vulnerabilidad y poder subir archvos a la máquina:
![[Mis apuntes/ANEXOS/Pasted image 20230227124040.png]]

Por tanto vamos a seguir estos pasos; nos registraremos:
![[Mis apuntes/ANEXOS/Pasted image 20230227124118.png]]

Y ahora, dentro de la parte de personal options, tenemos un panel donde podemos realizar algunas configuraciones y también subir archivos:
![[Mis apuntes/ANEXOS/Pasted image 20230227124155.png]]

Ahora vamos a crear un fichero .php malicioso para subirlo a la web y conseguir ejecución remota de comandos:
```php
<?php
        echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";
?>
```
![[Mis apuntes/ANEXOS/Pasted image 20230227124503.png]]

Ahora que ya lo hemos subido, vamos a hacer fuzzing para ver dónde se almacen los archivos subidos en esta web:
![[Mis apuntes/ANEXOS/Pasted image 20230227124652.png]]

Y nos encuentra el directorio uploads:
![[Mis apuntes/ANEXOS/Pasted image 20230227124711.png]]

Y si vamos a este directorio, nos encontramos con el archivo php malicoso que acabamos de subir:
![[Mis apuntes/ANEXOS/Pasted image 20230227124736.png]]

Y ahora que ya tenemos el nombre y la ubicación de este fichero php malicioso, vamos a probar en llamarlo desde la barra de búsqueda y ejecutando un comando determinado; donde veremos que funciona:
![[Mis apuntes/ANEXOS/Pasted image 20230227124916.png]]

De todos modos si intentamos obtener una reverse shell de esta forma, nos va a dar problemas, por lo que vamos a hacerlo creando un payload de msfvenom:
[[Mis apuntes/Ciberseguridad/Hacking/Hacking Generico/Msfvenom#Fichero PHP malicioso con msfvenom]]
![[Mis apuntes/ANEXOS/Pasted image 20230227130140.png]]

Lo compartimos con la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230227130204.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230227130238.png]]

Y si hacemos un ls vemos que ya lo tenemos:
![[Mis apuntes/ANEXOS/Pasted image 20230227130254.png]]

Y ahora si llamamos a este fichero desde la ruta uploads, vemos que habremos recibido la shell reversa con netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230227130613.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230227130624.png]]

Ejecutamos el comando script /dev/null -c bash para obtener un prompt, pero vemos que perdemos la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20230227130810.png]]

Por lo que vamos a ponernos en escucha mejor con metasploit con estas configuraciones:
![[Mis apuntes/ANEXOS/Pasted image 20230227130947.png]]

Y ahora si lanzamos la url desde el navegador, llamando al fichero virus.php malicioso, vemos que obtenemos la reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230227131029.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230227131036.png]]

Y ahora para ganar una shell de verdad escribiremos el script /dev/null -c bash:
![[Mis apuntes/ANEXOS/Pasted image 20230227131129.png]]

Una vez dentro, podemos conocer la versión de ubuntu con el comando lsb_release -a:
![[Mis apuntes/ANEXOS/Pasted image 20230227131356.png]]

Y si miramos por internet nos encontramos con un exploit que nos permite elevar nuestros privilegios en estas versiones de ubuntu:
![[Mis apuntes/ANEXOS/Pasted image 20230227131501.png]]

No obstante este exploit no va a funcionar, por lo que tenemos que investigar con una herramienta que sirve para detectar vulnerabilidades para escalar privilegios si lo ejecutamos en linux; y se llama linux-exploit-suggester:
![[Mis apuntes/ANEXOS/Pasted image 20230227133025.png]]

Hacemos un git clone y compartimos este script con la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230227133055.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230227133105.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230227133121.png]]

Y ahora desde la máquina víctima otorgamos permisos y lo ejecutamos:
![[Mis apuntes/ANEXOS/Pasted image 20230227133143.png]]

Y nos devuelve los fallos de seguridad que va detectando; y entre ellos tenemos el que encontramos uno parecido al que hemos encontrado antes por internet:
![[Mis apuntes/ANEXOS/Pasted image 20230227133237.png]]

Vamos a este link y lo descargamos:
![[Mis apuntes/ANEXOS/Pasted image 20230227133312.png]]

Lo compartimos con la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230227133523.png]]

Y ahora lo descargamos desde la máquina víctima, pero es importante hacerlo desde el directorio /tmp para contar con los permisos necesarios:
![[Mis apuntes/ANEXOS/Pasted image 20230227134041.png]]

Tenemos que compilarlo para poder ejecutarlo con el comando gcc:
![[Mis apuntes/ANEXOS/Pasted image 20230227134127.png]]

Y lo ejecutamos:







