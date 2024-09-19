# Interactuar pagina de inicio
```JavaScript
curl -X GET 192.69.173.3
```
![[Pasted image 20240522085545.png]]

# Interactuar metodo POST
```JavaScript
curl -X POST 192.69.173.3
```
![[Pasted image 20240522085624.png]]

# Obtener información encabezado
```JavaScript
curl -I 192.69.173.3
```
![[Pasted image 20240522085648.png]]

# Opciones permitias de curl
```JavaScript
curl -X OPTIONS 192.69.173.3 -v
```
![[Pasted image 20240522085737.png]]

# Pasar usuario y contraseña en pagina login
```JavaScript
curl -X POST 192.69.173.3/login.php -d "name=eric&password=password" -v
```
![[Pasted image 20240522085926.png]]

# Cargar fichero
```JavaScript
curl 192.69.173.3/uploads/ --upload-file hello.txt
```
![[Pasted image 20240522090030.png]]

# Eliminar  fichero
```JavaScript
curl -XDELETE 192.69.173.3/uploads/hello.txt
```
![[Pasted image 20240522090118.png]]


