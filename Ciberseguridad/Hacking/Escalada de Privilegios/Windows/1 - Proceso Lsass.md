LSASS mantiene una base de datos de cuentas de usuario locales y de dominio y gestiona su acceso y permisos. También administra la creación y eliminación de cuentas y contraseñas de usuario. Por ejemplo podemos obtener hashes de los usuarios:
![[Mis apuntes/ANEXOS/Pasted image 20230731090942.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230731090952.png]]

Si quisiéramos crackear estos hashes, podemos poner el metasploit en segundo plano y ejecutar el siguiente módulo:
```bash
use exploit/windows/http/badblue_passthru
```
![[Mis apuntes/ANEXOS/Pasted image 20230801130130.png]]

Establecemos un diccionario:
```bash
set CUSTOM_WORDLIST /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
```

Y lo ejecutamos:
![[Mis apuntes/ANEXOS/Pasted image 20230801130227.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230801130238.png]]
