El primer paso será instalar ssh de esta forma:
```mixed
sudo apt install openssh-server
```
![[Mis apuntes/ANEXOS/Pasted image 20230106072934.png]]

Después utilizaremos este comando para comprobar el estado de ejecución de SSH; y deberíamos verlo en ejecución:
```mixed
sudo systemctl status ssh
```

![[Mis apuntes/ANEXOS/Pasted image 20230106073030.png]]

Y por último podemos asegurarnos de que permanezca activado con este comando:
![[Mis apuntes/ANEXOS/Pasted image 20230106073115.png]]
Ahora tendremos que configurar el firewall para que permita conexiones por SSH sin problema; y para ello creamos esta regla utilizando este comando:
```mixed
sudo ufw allow ssh
```

![[Mis apuntes/ANEXOS/Pasted image 20230106073309.png]]

Y ahora sólo tenemos que reiniciar el servicio SSH para aplicar todos estos cambios; para ello utilizaremos este comando:
```mixed
sudo service ssh restart
```

![[Mis apuntes/ANEXOS/Pasted image 20230106073355.png]]

Ahora vamos a probarlo desde otro equipo poniendo la IP del equipo donde estamos configurando el servicio SSH y poniendo el username:
![[Mis apuntes/ANEXOS/Pasted image 20230106073456.png]]



