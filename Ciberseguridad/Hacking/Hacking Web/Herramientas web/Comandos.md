#### Tecnologias web
whatweb [IP]
![[Pasted image 20240305075259.png]]


http [IP]
![[Pasted image 20240305075324.png]]

#### Ataque diccionario listar directorios
dirb http://[IP]
![[Pasted image 20240305075500.png]]

dirb http://[IP] /usr/share/metasploit-framework/data/wordlists/directory.txt
![[Pasted image 20240305091957.png]]

browsh --startup-url http://[IP]/URL
![[Pasted image 20240305075644.png]]


lynx http://[IP]
lynx http://192.53.227.3
![[Pasted image 20240305090940.png]]
![[Pasted image 20240305090911.png]]


curl [IP] | more
![[Pasted image 20240305091150.png]]

wget "http://[IP]/index"
![[Pasted image 20240305091228.png]]

cat index | more
![[Pasted image 20240305091406.png]]