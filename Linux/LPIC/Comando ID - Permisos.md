Con este comando podré consultar los permisos que dispongo con el usuario que soy, por ejemplo si lo ejecuto siendo el usuario normal veremos esto:
![[Mis apuntes/ANEXOS/Pasted image 20230111205405.png]]

Siendo este usuario por ejemplo no podremos ver el fichero /etc/shadow con las contraseñas cifradas:
![[Mis apuntes/ANEXOS/Pasted image 20230111205518.png]]

Y si lo ejecuto siendo el usuario sudo, aquí veré que tengo permiso para hacer todo:
![[Mis apuntes/ANEXOS/Pasted image 20230111205432.png]]

Ahora sin embargo ya sí podré leer el fichero /etc/shadow:
![[Mis apuntes/ANEXOS/Pasted image 20230111205604.png]]