
# Enumerar nombre de usuario y maquina
`sysinfo`
![[Pasted image 20240507073837.png]]

`hostname`
`cat /etc/issue`
`cat /etc/*release`
![[Pasted image 20240507073838.png]]

`uname -a`
![[Pasted image 20240507074016.png]]

`env`
![[Pasted image 20240507074053.png]]

# Obtener información de la CPU
`lscpu`
![[Pasted image 20240507074409.png]]

# Listar información particiones
df -h
![[Pasted image 20240507074500.png]]

`df -ht ext4`
![[Pasted image 20240507074900.png]]

`lsblk | grep sd`
![[Pasted image 20240507075023.png]]
# Mostrar consumo de RAM
free -h
![[Pasted image 20240507074607.png]]

# Mostrar paquetes instalados
`dpkg -l`
![[Pasted image 20240507075159.png]]