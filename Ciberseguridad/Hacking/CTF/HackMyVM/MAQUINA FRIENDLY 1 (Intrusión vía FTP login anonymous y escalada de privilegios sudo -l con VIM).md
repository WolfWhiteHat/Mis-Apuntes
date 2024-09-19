Hacemos el reconocimiento de nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230708115833.png]]
Vemos el puerto FTP abierto y con anonymous FTP login allowed abierto, por lo que entramos y vemos un archivo index.html dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230708120006.png]]
Y si analizamos el contenido nos encontramos con que es una plantilla de apache:
![[Mis apuntes/ANEXOS/Pasted image 20230708120101.png]]
La misma que hay en el puerto 80:
![[Mis apuntes/ANEXOS/Pasted image 20230708120113.png]]
Adquirimos el php-reverse-shell.php de pentestmonkey, lo editamos y lo subimos a la máquina víctima vía FTP:
![[Mis apuntes/ANEXOS/Pasted image 20230708120423.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230708120513.png]]
Y ahora si desde la web lo ejecutamos, habremos recibido una reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230708120541.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230708120548.png]]
Y si hacemos un sudo -l vemos que podemos ejecutar vim como root:
![[Mis apuntes/ANEXOS/Pasted image 20230708120650.png]]
Por tanto ejecutamos VIM como root:
![[Mis apuntes/ANEXOS/Pasted image 20230708120822.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230708120843.png]]
Y ahora a continuación si damos a enter se habrá guardado lo de antes; y si luego hacemos clic en escape y volvemos a hacer shift y dos puntos para escribir shell, ya nos lanzará una bash de root, por tanto damos a enter y lo tenemos:
![[Mis apuntes/ANEXOS/Pasted image 20230128140352.png]]
Damos a enter y ya somos root:
![[Mis apuntes/ANEXOS/Pasted image 20230708121009.png]]
