Homebrew es un sistema de gestión de paquetes para instalar todo lo que tu ordenador no tiene instalado por defecto, es lo mismo que apt-get en Linux

https://franyerverjel.com/blog/instalacion-de-homebrew-en-mac

# Antes de instalar brew instalaremos xcode
Xcode es un entorno de desarrollo
xcode-select --install

# Instalar brew
```Bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

# Solucionar problema PATH
**Warning**: /opt/homebrew/bin is not in your PATH.
```Bash
export PATH=/opt/homebrew/bin:$PATH
```

# Solucionar problemas no instala brew

Pasos a seguir para solucionar el problema

Zsh, o Z Shell, es un intérprete de comandos o shell diseñado para sistemas operativos tipo Unix. Es una mejora y expansión del shell original de Bourne (sh) con características avanzadas y una sintaxis más robusta. 

Un intérprete es como un traductor que ayuda a que una computadora entienda y ejecute los comandos que le das. En lugar de hablar el lenguaje cotidiano que usamos, como el inglés o el español, las computadoras entienden instrucciones especiales llamadas "comandos". Estos comandos pueden ser escritos en un lenguaje que las computadoras comprenden.

El intérprete toma esos comandos escritos por un usuario y los convierte en acciones que la computadora puede realizar. Por ejemplo, si escribes un comando para copiar un archivo, el intérprete se encarga de llevar a cabo esa acción en la computadora.

# Saber que interprete estamos utilizando
```Bash
echo $SHELL
```

# Editar fichero con nano
```Bash
nano ~/.zprofile
```

## Añadir configuración del PATH
guardamos y salimos
```Bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```
![[Pasted image 20240524101309.png]]

# Recarga el achivo del perfil
```Bash
source ~/.zprofile
```

# Comprobar que esta bien instalado
```Bash
brew doctor
```

# Instalar programas externos
```
brew install "nombre del programa"
```