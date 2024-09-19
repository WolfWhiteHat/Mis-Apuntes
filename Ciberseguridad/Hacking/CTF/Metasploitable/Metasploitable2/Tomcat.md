Tomcat es un servidor web de código abierto. Es uno de los servidores web más populares del mundo y se utiliza para alojar una amplia variedad de aplicaciones web, desde sitios web estáticos hasta aplicaciones empresariales complejas.

Vamos a continuar explotando la siguiente vulnerabilidad, en este caso vamos a explotar un servidor apache tomcat que nos especifica que esta en el puerto 8180, si vamos al navegador, esccribimos la ip, en este caso 192.168.60.3:8180 estaremos accediendo al servidor en el cual ya estamos viendo que la versióne es la 5.5

![[Pasted image 20240130091001.png]]

Buscamos dentro de metasploit los exploits que tiene tomcat 5.5
![[Pasted image 20240130093906.png]]

Configuramos los parametros, en este caso especificaremos la ip del servidor, el puerto y un user y passwd por defecto que suele venir con tomcat
![[Pasted image 20240130094451.png]]

Revisamos toda la configuración y realizamos el ataque
![[Pasted image 20240130094121.png]]

Aquí podemos comprobar que ya hemos accedido y que tenemos acceso a todo el sistema desde terminal
![[Pasted image 20240130094227.png]]

