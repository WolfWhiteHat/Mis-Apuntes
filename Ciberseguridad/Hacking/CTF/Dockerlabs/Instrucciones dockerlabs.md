
Primero necesitamos tener instalado docker
```Bash
sudo apt-get install docker.io
```
![[Pasted image 20240522132945.png]]

Ahora para ejecutar una maquina la descargamos de la web de dockerlabs
https://dockerlabs.es/#/

Una vez descargado ejecutamos el siguiente comando
```
sudo bash auto_deploy.sh trust.tar
```
![[Pasted image 20240522133017.png]]

Una vez finalizada la maquina tecleando CTRL + C saldremos de la maquina y se eliminara automaticamente del sistema
![[Pasted image 20240522133048.png]]

# Comandos resolución problemas
```Bash
sudo systemctl restart docker
```

```Bash
sudo docker stop
```

```Bash
sudo docker container prune --force
````