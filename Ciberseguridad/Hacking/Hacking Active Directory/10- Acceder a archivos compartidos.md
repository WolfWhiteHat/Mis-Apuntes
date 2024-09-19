# SMB/CIFS
Primero tenemos que tener instalado `cifs-utils` para poder montar comparticiones SMB/CIFS
```
sudo apt update
sudo apt install cifs-utils
```

Ahora cremos un punto de montaje
```
sudo mkdir /mnt/Share
```

Montamos la compartición SMB/CIFS
```
sudo mount -t cifs //IP_del_servidor/nombre_de_la_comparticion /mnt/Share -o username=usuario,password=contraseña
```

Y ya podriamos acceder a los archivos y manipularlos
```
cd /mnt/Share
ls
```

Una vez terminemos desmontamos la particion
```
sudo umount /mnt/Share
```

-------

# NFS
Ahora pasamos a enumerar el servicio RPC Y NFS para ello usaremos `rpcinfo` 
```
rpcinfo -p 10.10.63.23
```
![[Pasted image 20240726113556.png]]

Encontramos que hay un directorio compartido el cual tiene los permisos que cualquiera puede acceder
```
showmount -e 10.10.92.58
```
![[Pasted image 20240726111742.png]]

Creamos una carpeta y lo montamos en nuestro sistema
![[Pasted image 20240726124648.png]]

Listamos la carpeta y encontramos los siguientes ficheros
![[Pasted image 20240726124746.png]]

----
# Acceder a recurso compartido desde ficheros
```
smb://10.10.25.146/
```
![[Pasted image 20240731112345.png]]