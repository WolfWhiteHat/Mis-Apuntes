## Instalación docker
Primero actualizamos el sistema
sudo apt update
sudo apt upgrade


Instala los paquetes necesarios para permitir que apt utilice un repositorio sobre HTTPS
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
![[Pasted image 20231113192929.png]]

Agrega la clave GPG oficial de Docker:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
![[Pasted image 20231113193020.png]]

Añade el repositorio de Docker al sistema:
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
![[Pasted image 20231113193115.png]]

Volvemos a actualizar los paquetes
sudo apt-get update

Instala la última versión de Docker Engine y Docker CLI:
sudo apt-get install docker-ce docker-ce-cli containerd.io
![[Pasted image 20231113193250.png]]

Verifica que Docker se haya instalado correctamente ejecutando el siguiente comando:
sudo docker run hello-world
![[Pasted image 20231113193402.png]]

Version de docker
docker --version
![[Pasted image 20231113195438.png]]

