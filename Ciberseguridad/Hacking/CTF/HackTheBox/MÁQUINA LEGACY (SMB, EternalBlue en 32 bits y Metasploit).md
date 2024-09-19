Lo primero será hacer los escaneos de siempre:
![[Mis apuntes/ANEXOS/Pasted image 20230323033124.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230323033126.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230323033129.png]]
Podemos ver cómo tiene el servicio SMB activo, por lo que vamos a comprobar con crackmapexec
para examinar este servicio:
![[Mis apuntes/ANEXOS/Pasted image 20230323033136.png]]
Estamos viendo como esta máquina es vulnerable a EternalBlue con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230323033142.png]]
Ahora podemos lanzar el exploit de eternalblue con metasploit y ganar acceso a la máquina:[[EternalBlue]]
![[Mis apuntes/ANEXOS/Pasted image 20230323033149.png]]
Vamos probando los payloads, y para 32 bits funciona el 1:
![[Mis apuntes/ANEXOS/Pasted image 20230323033157.png]]
Establecemos la IP del objetivo:
![[Mis apuntes/ANEXOS/Pasted image 20230323033203.png]]
Y ponemos ahora la IP nuestra para recibir la reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230323033210.png]]
Y con el comando run lanzamos el ataque:
![[Mis apuntes/ANEXOS/Pasted image 20230323033216.png]]
Y ya estamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230323033224.png]]
Una vez dentro vamos aesta ruta, y ya podremos acceder al escritorio:
![[Mis apuntes/ANEXOS/Pasted image 20230323033235.png]]
Y aquí tenemos la flag:
![[Mis apuntes/ANEXOS/Pasted image 20230323033246.png]]