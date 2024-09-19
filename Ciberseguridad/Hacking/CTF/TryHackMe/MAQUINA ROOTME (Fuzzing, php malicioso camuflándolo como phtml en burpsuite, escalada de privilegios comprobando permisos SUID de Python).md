Haremos los reconococimientos de nmap y vemos el puerto 80 y 22 abiertos:
![[Mis apuntes/ANEXOS/Pasted image 20230401011056.png]]

Si vemos la web es esta:
![[Mis apuntes/ANEXOS/Pasted image 20230401011433.png]]

Si hacemos fuzzing nos encontramos con un directorio de panel y otro de uploads:
![[Mis apuntes/ANEXOS/Pasted image 20230401011851.png]]

En el directorio de panel tenemos un lugar donde subir archivos:
![[Mis apuntes/ANEXOS/Pasted image 20230401011932.png]]

Si subimos un fichero .php malicioso nos va a dar error, pero el truco será en interceptar la petición web y así poder cambiar la extensión del fichero php por un phtml:
```python
<?php
        echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";
?>
```
![[Mis apuntes/ANEXOS/Pasted image 20230401013139.png]]

Y entonces ahora podremos subirlo y llamar a este archivo para obtener ejecución remota de comandos:
![[Mis apuntes/ANEXOS/Pasted image 20230401013213.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401013225.png]]

Ahora nos creamos un servidor web con python que aloje el código para enviarnos una reverse shell y después lo llamamos y pipeamos con curl:
![[Mis apuntes/ANEXOS/Pasted image 20230401014657.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401014615.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401014628.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401014638.png]]

Si hacemos una búsqueda de los permisos SUID, vemos que Python se encuentra entre ellos:
![[Mis apuntes/ANEXOS/Pasted image 20230401015128.png]]

Y también vemos estos permisos para Python:
![[Mis apuntes/ANEXOS/Pasted image 20230401015233.png]]

Por tanto nos creamos un fichero de Python con un código que nos permita escalar privilegios:
![[Mis apuntes/ANEXOS/Pasted image 20230401015723.png]]

Lo compartimos con la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230401015746.png]]

Y lo ejecutamos para convertirnos en root:
![[Mis apuntes/ANEXOS/Pasted image 20230401015812.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230401015823.png]]
[[13 - Escalada de Privilegios con Python]]