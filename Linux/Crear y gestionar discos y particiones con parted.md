# Añadir disco al sistema
Primero añadimos el disco al sistema

Visualizamos los discos
![[Pasted image 20240626102502.png]]

Seleccionamos la partición a formatear
![[Pasted image 20240626102608.png]]

Si el disco es nuevo es necesario crear una tabla de particiones, como vemos no tiene tabla de particiones
![[Pasted image 20240626102703.png]]

Creamos la tabla de particiones
```
mklabel 
```
![[Pasted image 20240626102726.png]]

Y ahora creamos la particion
```
mkpart primary ext4 1MiB 100%
```
![[Pasted image 20240626102850.png]]
![[Pasted image 20240626103020.png]]

Salimos de parted y ahora modificaremos la pariticon con ext4
```
sudo mkfs.ext4 /dev/vdb1
```
![[Pasted image 20240626103845.png]]

Montamos la particion
```
sudo mkdir /mnt/Disc2
sudo mount /dev/vdb1 /mnt/Disc2
```
![[Pasted image 20240626104017.png]]

Para terminar añadiremos la particion al fichero `/etc/fstab` para que la particion se monte automaticamente al inciar el sistema, para ello primero leermos el UUID de la particion
```
sudo blkid /dev/vdb1
```
![[Pasted image 20240626104338.png]]

Y ahora añadimos la sigueinte linea al archivo
![[Pasted image 20240626104550.png]]

Y ahora al reiniciar como podemos ver la particion se monta automaticamente
![[Pasted image 20240626105519.png]]