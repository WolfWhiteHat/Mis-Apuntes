# Pasos previos
ara revisar el espacio del sistema ejecutaremos el siguiente comando
![[Pasted image 20240626082940.png]]

Antes de continuar tenemos que tener instalado parted
```
sudo apt-get update
sudo apt-get install parted
```
![[Pasted image 20240626083144.png]]

# Ajustes del sistema
![[Pasted image 20240626100835.png]]

![[Pasted image 20240626100901.png]]

# Ejecución modo rescate
Ahora para redimensionar el espacio seguiremos el siguiente proceso, primero descargaremos la imagen iso de kali linux para poder acceder en modo rescate, reiniciaremos la maquina ejecutando la imagen iso y accederemos a `advanced options`
![[Pasted image 20240626091003.png]]

Y ahora accederemos a `rescue mode`
![[Pasted image 20240626091107.png]]


Una vez hayamos accedido aparecera un menu como si fuera de instalación, avanzamos la configuración de red hasta que nos salga esta pantalla donde seleccionaremos el dispositivo de rescate
![[Pasted image 20240626093820.png]]

Ejecutamos la shell
![[Pasted image 20240626093842.png]]

Le damos a continuar
![[Pasted image 20240626093901.png]]

Y ya estaremos en la shell
![[Pasted image 20240626093926.png]]

Como vemos estamos en una BusyBox, es una shell mas basica, podemos utilizar `fdisk -l`para listar las particiones
![[Pasted image 20240626094251.png]]

Ahora ejecutamos el siguiente comando
```
e2fsck -f /dev/vbd2
```
![[Pasted image 20240626094650.png]]

- **`e2fsck`**: Es una utilidad para comprobar y reparar sistemas de archivos ext2/ext3/ext4.
- **`-f`**: Fuerza la comprobación del sistema de archivos incluso si parece estar limpio.
- **`/dev/vdb2`**: Especifica la partición que se va a comprobar.


Ahora abrimos parted
```
parted /dev/vdb
print
```
![[Pasted image 20240626095316.png]]

Eliminamos la particion de swap
![[Pasted image 20240626095839.png]]

Reajustamos el espacio de la partición
```
resizepart 2 51.7G
```
![[Pasted image 20240626100150.png]]

Creamos la particion swap
```
mkpart primary linux-swap 51.7GB 53.7GB
```
![[Pasted image 20240626100408.png]]

Salimos de parted
![[Pasted image 20240626100454.png]]

Formateamos la particion de swap
```
mkswap /dev/vdb3
```
![[Pasted image 20240626100535.png]]

Activamos la particion swap
```
swapon /dev/vdb3
```
![[Pasted image 20240626100622.png]]

Y para finalizar extendemos el sistema de archivos
```
resize2fs /dev/vdb2
```
![[Pasted image 20240626100726.png]]

Ahora al reiniciar la maquina ya tendremos las particiones reajustadas




