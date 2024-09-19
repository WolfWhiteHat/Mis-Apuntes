Comando: ssh nombreUsuario@hostname_o_direccionIP

Cambiar puerto SSH
https://www.labsmac.es/cambiar-el-puerto-por-defecto-de-ssh-en-mac/


sudo nano /etc/services

sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist

ssh -p NumeroPuerto usuario@NombreHost-o-DireccionIP