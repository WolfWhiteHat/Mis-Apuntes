Un Web Application Firewall (WAF) **protege de múltiples ataques al servidor de aplicaciones web en el backend**. La función del WAF es garantizar la seguridad del servidor web mediante el análisis de paquetes de petición HTTP / HTTPS y modelos de tráfico.

WAFW00F es una herramienta que nos permite identificar diferentes tipos de WAF a partir de sus huellas. Un WAF (Web Application Firewall) es un tipo específico de cortafuegos que protege contra ataques a aplicaciones web.



### Comandos
Con el comnado wafw00f -l podemos ver todos los firewalls que puede detectar la herramienta
wafw00f -l
![[Pasted image 20240313105258.png]]

Como podemos ver con el siguiente comando nos indicara si la pagina web la cual estamos investigando tiene de por medio un firewall o un proxy.
wafw00f hakcersploit.org
![[Pasted image 20240313105335.png]]

Si añadimos un -a podremos obtener mas información
wafw00f hackersploit.org -a
![[Pasted image 20240313105354.png]]