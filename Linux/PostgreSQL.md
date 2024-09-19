Instalamos/Actualizamos postgresql
![[Pasted image 20240304085545.png]]


Para utilizar la base de datos de PostgreSQL comenzaremos configurando el archivo postgresql.service
![[Pasted image 20240304085211.png]]
![[Pasted image 20240304085157.png]]

Reiniciamos el servicio de postgresql y daemon-reload
![[Pasted image 20240304085420.png]]


Asignamos permisos al usuario que ejecutara la base de datos
usermod -aG postgres root
![[Pasted image 20240304090417.png]]


Revisamos que los permisos se apliquen correctamente
![[Pasted image 20240304090538.png]]
