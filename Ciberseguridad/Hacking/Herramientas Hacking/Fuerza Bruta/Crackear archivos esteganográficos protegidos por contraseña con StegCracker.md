La herramienta `StegCracker` nos permite realizar ataques de fuerza bruta contra archivos esteganográficos protegidos por contraseña

```
git clone https://github.com/Paradoxis/StegCracker.git
```

# Instalar StegCracker
```
sudo apt install stegcracker
```
![[Pasted image 20240906113636.png]]

# Ejemplo de StegCracker
Ahora ejecutando el siguiente comando ejecutaríamos un ataque de fuerza bruta contra el fichero
```
stegcracker oneforall.jpg /usr/share/wordlists/rockyou.txt 
```
![[Pasted image 20240906113742.png]]


