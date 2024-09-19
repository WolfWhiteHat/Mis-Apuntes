Es un escaner de vulnerabilidades para wordpress el cual es capaz de enumerar todos los pluggins instalados


# Escaner pluggins y vulnerabilidades
```Bash
wpscan --url https://dominio.com/wordpress -e u vt
```
![[Pasted image 20240530095809.png]]

# Enumerar usuarios
```Bash
sudo wpscan --url https://dominio.com/wordpress -e u
```
![[Pasted image 20240530095854.png]]

# Ataque fuerza bruta usuarios
```Bash
sudo wpscan --url 192.168.1.10/wordpress -e U -P /home/kali/Documentos/diccionario
```

# Escaner avanzado con token
```Bash
wspcan --url https://wordpress.org --api-token <token>
```
