Hacemos los reconocimientos de nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230419171711.png]]
Vemos la web:
![[Mis apuntes/ANEXOS/Pasted image 20230419171425.png]]
Y ahora vamos a mirar el puerto 5601, donde vemos que también corre un servicio web de Kibana:
![[Mis apuntes/ANEXOS/Pasted image 20230419171826.png]]
Y si hacemos un whatweb veremos la versión de kibana:
![[Mis apuntes/ANEXOS/Pasted image 20230419171911.png]]
Y buscando por github encontramos un exploit y la vulnerabilidad pública:
![[Mis apuntes/ANEXOS/Pasted image 20230419172213.png]]
Y aquí tenemos las instrucciones donde nos dicen que si pegamos este payload dentro de la parte del Timelion visualizer, podremos ejecutar un comando remotamente:
![[Mis apuntes/ANEXOS/Pasted image 20230419193826.png]]
Por tanto nos ponemos en escucha con netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230419194613.png]]
Y mandamos el payload, mejor el segundo, el de chiveta:
![[Mis apuntes/ANEXOS/Pasted image 20230419195137.png]]
Y aquí hemos recibido la reverse shell:![[Mis apuntes/ANEXOS/Pasted image 20230419195157.png]]
Anteriormente habíamos visto que en la web nos hacían mención a algo de capabilities, por lo que podemos hacer una búsqueda de las capabilities del sistema en linux con el comando getcap -r / 2>/dev/null:
![[Mis apuntes/ANEXOS/Pasted image 20230419201058.png]]
Nos encontramos con un directorio quue se llama hackmeplease donde podemos ejecutar Python, por lo que nos ubicamos dentro de este directorio y ejecutamos este comando:
![[Mis apuntes/ANEXOS/Pasted image 20230419201222.png]]
```python
./python3 -c 'import os; os.setuid(0); os.system("/bin/sh")'
```
Lo ejecutamos dentro de este directorio y ya nos convertimos en root:


