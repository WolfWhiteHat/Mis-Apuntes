# Instalación QEMU
Ahora instalaremos qemu, lo utilizararemos para poder convertir los formatos de Virtual Box .vmdk a formato UTM
```Bash
brew install qemu
```

# Ubicación maquinas
~/ericmoliner/Biblioteca/Containers/UTM/Data/Documents/Maquina
![[Pasted image 20240918115042.png]]

# Transferir maquinas a formato QCOW2
# Extraer fichero ova
Primero descomprimimos el archivo .ova
```Bash
tar -xvf maquina.ova
```
![[Pasted image 20240918115112.png]]

# Convertir archivo vmdk a formato UTM
```Bash
qemu-img convert -O qcow2 -c ./archivo.vmdk ./archivo.qcow2
```

```Bash
qemu-img convert -O qcow2 -c ./metasploitable3-ub1404-disk001.vmdk ./metasploitable3-ub1404-disk001.qcow2
```
![[Pasted image 20240918115155.png]]

# Importar maquina virtual UTM
Una vez tengamos el fichero qcow2 pasaremos a crear la maquina virtual, primero seleccionaremos Emular
![[Pasted image 20240129082455.png|300]] 

Continuaremos dandole a Otro
![[Pasted image 20240129082604.png|300]]

![[Pasted image 20240129082639.png|300]]

![[Pasted image 20240129083037.png|300]]

![[Pasted image 20240129083216.png|300]]

# Configuración maquina UTM
Ahora tendremos que cambiar un par de parametros antes de poder ejecutar la maquina de Metasploitable, primero quitamos el arranque UEFI
![[Pasted image 20240129083317.png|500]]

Y cambiaremos el disco IDE e importaremos el archivo qcow2 creado previamente
![[Pasted image 20240129083554.png|400]]

-------
# Transferir maquinas a formato VMDK
Primero localizamos el archivo de imagen de disco en formato qcow2, para ello vamos a la ruta donde se encuentre la maquina UTM, una vez encontrada damos click derecho y seleccionamos mostrar contenido del paquete
![[Pasted image 20240610122748.png|250]]

Una vez dentro accedemos a data y encontraremos la imagen de la maquina en formato qcow2
![[Pasted image 20240610122859.png|250]]

Ahora ejecutaremos el siguiente comando para convertir la maquina en formato VMDK
```Bash
qemu-img convert -f qcow2 -O vmdk 8CA5392F-7ED1-4E75-A338-AADD9BCD365A.qcow2 /Users/Name_User/hacker.vmdk
```
![[Pasted image 20240918115249.png]]

Y ya tendriamos el archivo en la ruta con el nuevo formato
![[Pasted image 20240918115342.png]]

# Importar maquina virtual VMware
Seleccionamos Create a custom virtual machine
![[Pasted image 20240610123712.png|500]]

Seleccionamos el sistema operativo
![[Pasted image 20240610123814.png]]

Ahora seleccionamos la imagen que tenemos de la maquina a importar
![[Pasted image 20240918115411.png]]
![[Pasted image 20240610125250.png]]

Revisamos la configuración y le damos a finalizar
![[Pasted image 20240610125320.png]]


https://dev.to/merlos/how-to-setup-metasploitable-in-a-mac-with-m1-chip-44ph