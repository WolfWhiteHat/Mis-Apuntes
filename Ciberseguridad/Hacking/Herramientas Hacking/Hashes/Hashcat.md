Hashcat es una herramienta de código abierto para recuperar contraseñas. Es compatible con una amplia variedad de algoritmos de hash, incluyendo MD5, SHA1, SHA256 y bcrypt. Hashcat también puede utilizar tarjetas gráficas para acelerar el proceso de recuperación de contraseñas.

Hashcat se puede utilizar para una variedad de propósitos, incluyendo:
- Recuperar contraseñas perdidas u olvidadas.
- Auditar la seguridad de una red.
- Proteger los datos contra el acceso no autorizado.

# Tutorial Hashcat
Primero necesitamos un fichero en el cual este nuestro hash
![[Pasted image 20240214105512.png]]
Ahora vamos a descifrar este hash con la herramienta hashcat, para ello necesitaremos utilizar un diccionario, una vez lo tenemos ejecutaremos el siguiente comando
```Bash
hashcat -m 0 -a 0 -o resultado.txt contraseña.txt rockyou.txt
```
 - m para indicar el hash que queremos crackear y 0 para el tipo de hash
- a el modo de ataque que vamos a realizar 
- o para exportar el resultado en un fichero
![[Pasted image 20240214112115.png]]

Como podemos ver la herramienta se ha ejecutado correctamente y en la sigueinte imagen se puede ver como  ha creado el fichero me indica el hash y al lado la contraseña haseada
![[Pasted image 20240214112252.png]]

Ahora vamos ha hacer los mismos pasos pero para hashea una contraseña SHA1

Realizamos el mismo proceso, el comando es el siguiente
```
hashcat -m 100 -a 0 -o resultado.txt contraseña.txt rockyou.txt
```

El unico cambio es el -m que ha pasado de 0 a 100 porque le estamos especificando que tipo de hash es
![[Pasted image 20240214112846.png]]


-----
Para que hashcat encuentre las credenciales de NTLM unicamente debemos pegarle el hash NTLM sin el user ni el hash LM
```
hashcat -m 1000 --force hash.txt /usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240722100225.png]]
![[Pasted image 20240722100258.png]]

Ahora podemos volver a listar la salida de hashcat con el siguiente comando
```
hashcat -m 1000 --show hash.txt
```
![[Pasted image 20240722101519.png]]