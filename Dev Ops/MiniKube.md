Minikube utiliza Docker para ejecutar los contenedores.

## Instalación MiniKube
Primero actualizamos el sistema
sudo apt update
sudo apt upgrade

Después ejecutamos snap install kubectl, como no podiamos instalarlo desde apt, hemos utilizado el repositorio de snap
![[Pasted image 20231113192036.png]]

Verificamos que esta bien instalado
kubectl version --client
![[Pasted image 20231113192301.png]]

Descarga el binario de Minikube y cárgalo en tu sistema:
![[Pasted image 20231113192420.png]]

Otorga permisos de ejecución al binario:
chmod +x minikube-linux-arm64
![[Pasted image 20231113192526.png]]

Mueve el binario a un directorio incluido en tu variable de entorno `PATH`, por ejemplo:
sudo mv minikube-linux-arm64 /usr/local/bin/minikube
![[Pasted image 20231113192612.png]]

Iniciamos minikube
![[Pasted image 20231113194053.png]]

Verificamos que este bien instalado
minikube status
![[Pasted image 20231113194208.png]]

También podemos verificarlo con el siguiente comando
kubectl cluster-info
![[Pasted image 20231113194305.png]]
Esto  muestra la información del clúster, indicando que estás conectado a Minikube.
