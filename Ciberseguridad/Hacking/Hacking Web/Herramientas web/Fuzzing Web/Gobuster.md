Gobuster es una herramienta de enumeración y fuzzing web que permite encontrar archivos y directorios dentro de un servidor web. 
Gobuster tiene tres modos disponibles. “dir”, el modo clásico de fuerza bruta contra directorios, “dns”, el modo de fuerza bruta contra subdominios DNS, y “vhost”, el modo de fuerza bruta contra hosts virtuales (no es lo mismo a “DNS”).

# Directorio diccionario Gobuster
`/usr/share/wordlists/dirbuster/

# Fuzzing de directorios y extension de archivos
```python
gobuster dir -u http://example.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x xml,py,php,html -t 200
```

# Fuzzing de subdominios
```Python
gobuster vhost --append-domain -u http://creative.thm/ -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -k -t 40
```
- `vhost`: Especifica que el escaneo se realizará en modo virtual host, lo que significa que `gobuster` intentará enumerar subdominios utilizando la técnica de "Host: header".
- `--append-domain`: Añade el dominio especificado (`http://creative.thm/`) al final de cada subdominio en la lista proporcionada, facilitando la construcción completa del subdominio que será probado.
- `-k`: Esta opción indica a `gobuster` que ignore los errores de certificado SSL/TLS, lo cual es útil si el sitio utiliza HTTPS con un certificado auto-firmado o no válido.
- `-t 40`: Define el número de hilos o conexiones simultáneas que `gobuster` utilizará para realizar las solicitudes al servidor. En este caso, se están utilizando 40 hilos, lo que puede acelerar el escaneo pero también aumentar la carga en el servidor objetivo.

# Fuzzing de subdominios dns
```python
gobuster dns -d example.com -w /ruta_diccionario/subdomains-top1million-110000.txt
```

- `dns`: Indica que el modo de escaneo será para DNS, es decir, `gobuster` intentará enumerar subdominios consultando registros DNS.
- `-d example.com`: Especifica el dominio que se va a escanear. En este caso, el dominio es `example.com`.



