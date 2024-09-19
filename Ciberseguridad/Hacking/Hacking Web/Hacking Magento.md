Vamos a utilizar este repositorio de github para montar el laboratorio de pruebas:
![[Mis apuntes/ANEXOS/Pasted image 20230423082003.png]]
Lo ejecutamos con docker compose:
![[Mis apuntes/ANEXOS/Pasted image 20230423082210.png]]
Y ya tenemos el magento corriendo por el puerto 8080:
![[Mis apuntes/ANEXOS/Pasted image 20230423082315.png]]
Y aquí ponemos esta configuración (en password ponemos root):
![[Mis apuntes/ANEXOS/Pasted image 20230423082422.png]]
Y aquí dentro del directorio /admin se encontrará el panel de administración:
![[Mis apuntes/ANEXOS/Pasted image 20230423082505.png]]
Y llegamos al panel de login:
![[Mis apuntes/ANEXOS/Pasted image 20230423082700.png]]
Y vamos a explotar una SQL injection, donde tendremos este script que nos automatiza todo este proceso:
![[Mis apuntes/ANEXOS/Pasted image 20230423082809.png]]
Iniciamos sesión dentro del magento:
![[Mis apuntes/ANEXOS/Pasted image 20230423083220.png]]
Y ahora si lanzamos este script, podrá hacer un robo de cookies de sesión:
![[Mis apuntes/ANEXOS/Pasted image 20230423083317.png]]
Y desde la extensión cookie editor tenemos este campo donde podemos poner una cookie de sesión:
![[Mis apuntes/ANEXOS/Pasted image 20230423083743.png]]
Le ponemos la nueva cookie que hayamos capturado:
![[Mis apuntes/ANEXOS/Pasted image 20230423083819.png]]
Recargamos la página y ya estamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230423083844.png]]
## HERRAMIENTA PARA ENUMERAR MAGENTO
Tenemos una herramienta llamada magscan:
![[Mis apuntes/ANEXOS/Pasted image 20230423084831.png]]
Nos clonamos el proyecto:
![[Mis apuntes/ANEXOS/Pasted image 20230423084924.png]]
Y nos pide también que descarguemos un archivo con extensión .phar:
![[Mis apuntes/ANEXOS/Pasted image 20230423084950.png]]
Y ahora con php le pasamos este archivo y ya lo tenemos todo listo:
![[Mis apuntes/ANEXOS/Pasted image 20230423085101.png]]
Y así le lanzamos un escaneo:
![[Mis apuntes/ANEXOS/Pasted image 20230423085154.png]]
