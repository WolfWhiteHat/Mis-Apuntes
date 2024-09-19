Glances es una herramienta de monitoreo multiplataforma escrita en Python que proporciona información en tiempo real sobre el uso del sistema, incluyendo CPU, memoria, disco, red y más. Es altamente personalizable y puede ejecutarse en modo servidor web, lo que permite acceder desde cualquier dispositivo con un navegador web. La instalación es sencilla utilizando `pip` o Docker. Soporta varios módulos de exportación para integración con otros sistemas de monitoreo como InfluxDB y Prometheus.

```
https://github.com/nicolargo/glances
https://nicolargo.github.io/glances/
```

# Requisitos previos
## **Instalar brew**
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## **Instalación python y pipx**
```
brew install python
brew install pipx
```

## **Instalar FastAPI**
```
pipx install fastapi uvicorn
```

## **Agregar pipx al PATH**
```
pipx ensurepath
```

## **Agregar al PATH en fichero zshrc**
```
nano ~/.zshrc
export PATH="$HOME/.local/bin:$PATH"
source ~/.bashrc
```

# Instalación Glances
```
pipx install glances
```

# Instalar dependencias interfaz web
```
pipx install 'glances[web]'
```

# Instalacion completa
```
pipx install --force 'glances[all]'
```

# Ejecutar Glances
```
glances
```
![[Pasted image 20240918114336.png]]

# Ejecutar Glances Web
```
glances -w
```
![[Pasted image 20240711103215.png]]
![[Pasted image 20240711103235.png]]

# Atajos
- `q`: Salir de Glances.
- `1`: Mostrar información detallada de cada CPU.
- `m`: Mostrar información de la memoria.
- `d`: Mostrar información del disco.
- `n`: Mostrar información de la red.
- `h`: Mostrar ayuda con más atajos de teclado.








