PATH es una variable de entorno en los sistemas operativos Unix y Linux que especifica los directorios donde el sistema operativo busca programas ejecutables. Cuando ejecutas un comando en la línea de comandos, el sistema busca ese comando en los directorios listados en la variable PATH.

# Añadir directorio a PATH temporalmente
```
export PATH=PATH$:/home/kali/.local/bin/
```
![[Pasted image 20240710082946.png]]

# Añadir directorio a PATH persistentemente
Para añadir un directorio de forma persistente tenemos que añadir la ruta del directorio a nuestro PATH, primero comprobamos la shell que estamos ejecutando
![[Pasted image 20240710083711.png]]

 Modificar el fichero `~/.zshrc.` y añadir el siguiente contenido
```
export PATH="$PATH:/home/kali/.local/bin/"
```
![[Pasted image 20240710083613.png]]

Aplicamos los cambios
![[Pasted image 20240710083850.png]]

Y al verificarlo podemos ver como esta añadido en el PATH
![[Pasted image 20240710084025.png]]



