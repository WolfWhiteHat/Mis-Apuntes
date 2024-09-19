Hacemos un escaneo de nmap
![[Pasted image 20240709072808.png]]

Accedemos al navegador y revisamos el servicio que esta abierto
![[Pasted image 20240709072921.png]]

Ahora realizaremos fuzzing web y enumeraremos los directorio y archivos ocultos
![[Pasted image 20240709074352.png]]

Revisamos el enlace de spip y encontramos la siguiente web
![[Pasted image 20240709074436.png]]

Accedemos al enlace de debajo donde pone Se connecter y accedemos a un portal de login
![[Pasted image 20240709074534.png]]

Revisamos y encontramos que es posible que haya una vulnerabilidad de LFI
![[Pasted image 20240709074802.png]]

Revisamos la version del CMS
![[Pasted image 20240709075707.png|500]]

No conseguimos encontrar acceso, revisamos vulnerabilidades sobre el CMS y encontramos el siguiente exploit
```
https://github.com/Chocapikk/CVE-2023-27372
```
![[Pasted image 20240709084528.png]]

Instalamos los requerimentos
![[Pasted image 20240709085202.png]]

Y al ejecutar el exploit ya obtenemos ejecución remota de comandos
```
python3 CVE-2023-27372.py -u http://10.10.128.134/spip/ -v -o report.txt
```
![[Pasted image 20240709085245.png]]

Leemos el fichero passwd y obtenemos los usuarios
![[Pasted image 20240709085426.png]]

Nos generamos una reverse shell
![[Pasted image 20240709085800.png]]

y ya tenemos acceso a la maquina victima
![[Pasted image 20240709085818.png]]

Revisando permisos nos encontramos que hay configurado ssh y tenemos acceso de lectura
![[Pasted image 20240709091418.png]]

Probamos a acceder y ya estamos dentro con el usuario de think
![[Pasted image 20240709091952.png]]

Revisando los permisos de los binarios encontramos que podemos ejecutar un programa para levantar contenedores
![[Pasted image 20240709094917.png]]

Revisamos el fichero y encontramos el binario que lo ejecuta
![[Pasted image 20240709100439.png]]

Revisamos la shell y encontramos que estamos utilizando ash
![[Pasted image 20240709102125.png]]

Obtenemos una sesión bash
```
cp /bin/bash /dev/shm
chmod +x /dev/shm/bash
/dev/shm/bash -p
id
ps -p $$
```
![[Pasted image 20240709103626.png]]

Ahora podemos modificar el binario `run_container.sh` para que cuando se ejecute obtengamos una bash como root
```
echo -e '#!' /bin/bash\n/bin/bash -ip' > /opt/run_container.sh
```
![[Pasted image 20240709103747.png]]

Y al ejecutar el binario obtenemos la bash como root
![[Pasted image 20240709103833.png]]

Obtención de la flag de root
![[Pasted image 20240709104325.png]]

