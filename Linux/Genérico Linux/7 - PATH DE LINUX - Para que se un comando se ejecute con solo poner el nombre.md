En Linux, el PATH es una variable de entorno que contiene una lista de directorios separados por dos puntos (:), donde el sistema busca los programas y comandos ejecutables cuando se escribe un comando en la terminal en cualquiera de las siguientes ubicaciones:
![[Mis apuntes/ANEXOS/Pasted image 20230218135938.png]]

Por ejemplo, si el directorio /usr/local/bin está incluido en el PATH, y hay un archivo ejecutable llamado "actualizar.sh" en ese directorio, se puede ejecutar ese programa desde cualquier directorio en la terminal simplemente escribiendo el nombre del programa:
![[Mis apuntes/ANEXOS/Pasted image 20230218140121.png]]

# AÑADIR DIRECTORIO AL PATH DE LINUX
No obstante, también podemos añadir un directorio determinado dentro del path de Linux exportando una variable de entorno de la siguiente forma:
```Bash
export PATH=$PATH/ruta/del/binario
```
![[Mis apuntes/ANEXOS/Pasted image 20230218140428.png]]

# Fichero que gestiona el PATH
Los ficheros que vemos a continuación son los que gestionan el PATH y se ejecutan cuando inicias sesión en un terminal, estos ficheros se encuentran en la raiz de los usuarios
- `.bashrc`
- `.bash_profile`
- `.zshrc`