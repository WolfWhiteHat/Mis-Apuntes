Dirsearch es una herramienta de código abierto utilizada para la enumeración de directorios y archivos en servidores web


# Escanear url
```Bash
dirsearch -u http://olympus.thm -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -e php,html, js
```
![[Pasted image 20240611130148.png]]
- -u: Para indicar la url
- -w: Para indicar el direcctorio de palabras
- -e: Para indicar los ficheros a analizar