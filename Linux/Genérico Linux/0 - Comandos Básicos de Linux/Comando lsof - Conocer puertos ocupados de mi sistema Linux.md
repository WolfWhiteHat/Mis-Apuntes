Por ejemplo ejecutamos un servidor web con Python por el puerto 80:

![[Mis apuntes/ANEXOS/Pasted image 20230127190239.png]]
 
Y ahora con el comando lsof -i:80 puero ver qué servicio está ocupando el puerto 80 de mi equipo:

  ![[Mis apuntes/ANEXOS/Pasted image 20230127190310.png]]
Si quisiera detener este servicio con lsof podría utilizar el comando kill -9 de esta forma:
![[Mis apuntes/ANEXOS/Pasted image 20230130113547.png]]
