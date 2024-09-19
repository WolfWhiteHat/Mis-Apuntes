Es importante para no dejar rastro en el sistema cargar todos los archivos en la carpeta Temp, si no esta creada la creamos
![[Pasted image 20240515093559.png]]

Ejecutamos un modulo para ganar persistencia, este modulo almacena en la maquina victima un payload, para borrar nuestro rastro en nuestra maquina de Kali se guarda un archivo para ejecutar
![[Pasted image 20240515094512.png]]

SI vamos a la ruta de arriba podemos ver el archivo en el sistema
![[Pasted image 20240515094916.png]]

Para borrar este registro ejecutaremos el siguiente comando
```Bash
resource /root/.msf4/logs/persistence/ATTACKDEFENSE_20240515.1310/ATTACKDEFENSE_20240515.1310.rc
```
![[Pasted image 20240515095318.png]]

De esta forma habremos borrado el fichero que nos ha creado una vez hemos terminado de explotar la maquina.


Otra forma mas radical de borrar nuestras huellas es ejecutando el comando que tiene meterprer `crearev` pero hay que tener en cuenta que esto borra todos los registros del sistema
![[Pasted image 20240515095507.png]]