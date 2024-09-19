Es una herramienta la cual podemos listar directorios, acceder a archivos, descargar y subir archivos y ejecución de comandos explotando el protocolo SMB
# Enumerar recursos compartidos en un servidor SMB
```python
smbmap -H <IP>
```

Por ejemplo, para enumerar los recursos compartidos en un servidor con la dirección IP 192.168.1.100, puede ejecutar el siguiente comando, el cual mostrará una lista de los recursos compartidos en el servidor, junto con información sobre los permisos de acceso.
```python
smbmap -H 192.168.1.100
```
![[Mis apuntes/ANEXOS/Pasted image 20230406074550.png]]

# Enumerar archivos y directorios en un recurso compartido
Podemos enumerar recursos compartidos sin proporcionar credenciales haciendo uso de una null session simplemente usando el parámetro -H:
![[Mis apuntes/ANEXOS/Pasted image 20230420110521.png]]

También podríamos conectarnos haciendo uso de una null session de esta forma:
```bash
smbmap -u "null" -H 10.10.182.108
```
![[Mis apuntes/ANEXOS/Pasted image 20230701103816.png]]

Si quisiéramos proporcionar credenciales, lo haríamos de esta forma:
```python
smbmap -H <IP> -u <username> -p <password> -s <sharename> -R
```

Por ejemplo, para enumerar los archivos y directorios en el recurso compartido "compartido1" en un servidor con la dirección IP 192.168.1.100, puede ejecutar el siguiente comando, el cual mostrará una lista de los archivos y directorios en el recurso compartido "compartido1", junto con información sobre los permisos de acceso.
```python
smbmap -H 192.168.1.100 -u usuario -p contrasena -r compartido1
```
![[Mis apuntes/ANEXOS/Pasted image 20230425162011.png]]

--- 
# EJEMPLO FUNCIONAMIENTO SMBMAP

Así sería el funcionamiento de smbmap
![[Mis apuntes/ANEXOS/Pasted image 20230213104857.png]]

# DESCARGAR UN ARCHIVO CON SMBMAP
Lo haríamos con el parámetro --download:
![[Mis apuntes/ANEXOS/Pasted image 20230727151919.png]]
