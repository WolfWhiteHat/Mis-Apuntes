OWASP ZAP (abr. para _Zed Attack Proxy_) es un escáner de seguridad web


# Realizar escaner con OWASP ZAP
Una vez arrancada la herramienta seleccionaremos Automated Scan y lo configuraremos
![[Pasted image 20240527081524.png]]

Como podemos ver a la izquierda aparece todas las URL que encuentra y el tipo de petición que se ha echo
![[Pasted image 20240527081918.png]]

Si continuamos abajo podremos trabajar con toda la información, el apartado de alertas muestra las posibles vulnerabilidades que haya detectado
![[Pasted image 20240527081807.png]]


# Escaner manual con OWASP ZAP
Para empezar realizando un escaneo de la web seleccionamos manual explorer
![[Pasted image 20240527080905.png]]

Seleccionamos la url, activamos enable HUD y a launch browser
![[Pasted image 20240527081001.png]]

Esto nos abrira el navegador con la herramienta abierta para ir analizando la web
![[Pasted image 20240527081106.png]]

Cada vez que realizamos una accción la herramienta recoge esa información, en este caso hemos echo un login en la web y podemos ver toda la información registrada
![[Pasted image 20240527081252.png]]

