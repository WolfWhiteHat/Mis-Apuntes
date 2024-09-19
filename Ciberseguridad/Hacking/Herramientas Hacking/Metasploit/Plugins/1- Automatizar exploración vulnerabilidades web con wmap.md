
Primero nos descargaremos el pluging de github y lo añadiremos al directorio 
/usr/share/metasploit-framework/plugins

https://github.com/yangsec888/wmap


una vez este añadido ejecutaremos la consola de metasploit y ejecutaremos el siguiente comando
load wmap
![[Pasted image 20240325175837.png]]


Una vez cargado el plugin lo primero es crear un sitio
wmap_sites -a 192.7.3.3
![[Pasted image 20240325180147.png]]


Continuaremos especificando la ip de la victima la direccion de origen
wmap_targets -t http://192.7.3.3
![[Pasted image 20240325180340.png]]


Verificar configuración
wmap_sites -l
wmap_tagrtest -l
![[Pasted image 20240325180449.png]]



Una vez configurado comprobaremos todos los modulos que van a ejecutarse
wmap_run -t
![[Pasted image 20240325180721.png]]


Ejecutamos todos los modulos
wmap_run -e
![[Pasted image 20240325180852.png]]


## Modulos Wmap

![[Pasted image 20240325181158.png]]![[Pasted image 20240325181236.png]]