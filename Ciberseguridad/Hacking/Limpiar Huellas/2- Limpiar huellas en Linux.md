Al igual que en Windows, los sistemas linux tienen una carpeta temporal que borra todos los ficheros una vez se reinicia el ordenador, esta carpeta esta en la raiz y es la carpeta `tmp`
![[Pasted image 20240516082319.png]]

También tenemos en la raiz dos archivos que son importantes a tener en cuenta, uno es el fichero `~/.bash_history` el cual almacena todo nuestro registro de comandos que vamos ejecutando, este fichero esta en la ruta del usuario.

El segundo fichero a tener en cuneta es `.ssh` este fichero almacena la configuración del servicio ssh.

Para eliminar el historial tenemos dos formas, una es ejecutando el siguiente comando
```Bash
history -c
```
![[Pasted image 20240516082542.png]]

Para usar un comando mas completo
```Bash
history -c && history -w
```

Para eliminar las pruebas por completo si el sistema esta bien configurado y tiene el fichero `.bash_history` podriamos acceder a el y borrar unicamente nuestros comandos para no dejar rastro ni sospechas de que el sistema ha sido manipulado

Para eliminar el fichero por completo podriamos ejecutar el siguiente comando
```Bash
cat /dev/null > ~/.bash_history
```

Para eliminar el historial y cerrar la conexión
```Bash
cat /dev/null > ~/.bash_history && history -c && exit
```
