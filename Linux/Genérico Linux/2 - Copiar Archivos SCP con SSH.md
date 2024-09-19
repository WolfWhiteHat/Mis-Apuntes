## Para descargar archivos del servidor
Lo haremos con scp utilizando este comando, primero poniendo la IP del servidor desde donde queremos bajarnos el archivo, y luego la ruta de nuestra máquina local donde lo queramos descargar:
![[Mis apuntes/ANEXOS/Pasted image 20230119184948.png]]
## Para subir archivos al servidor
Vamos a subir este archivo:
![[Mis apuntes/ANEXOS/Pasted image 20230119185202.png]]
Para ello ejecutamos el siguiente comando:
![[Mis apuntes/ANEXOS/Pasted image 20230119185251.png]]
Y ya lo tenemos subido:
![[Mis apuntes/ANEXOS/Pasted image 20230119185308.png]]
## Para subir una carpeta entera por SSH
Si queremos subir todos los archivos que estén dentro de una carpeta, lo haríamos de esta forma; aquí tenemos la carpeta:
![[Mis apuntes/ANEXOS/Pasted image 20230119185522.png]]
Y con este comando lo subiríamos todo, ya que con el asterisco indicamos que suba la totalidad de archivos, y con la opción -r que sea recursivo:
![[Mis apuntes/ANEXOS/Pasted image 20230119190046.png]]
Y aquí están:
![[Mis apuntes/ANEXOS/Pasted image 20230119190103.png]]
