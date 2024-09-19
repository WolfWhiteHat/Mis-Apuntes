El parámetro "--script" de Nmap se utiliza para especificar un conjunto de scripts que se ejecutarán durante un escaneo. 

El parámetro "--script" puede tomar un solo script como argumento, o puede especificar varios scripts separados por comas. También se pueden utilizar comodines para seleccionar múltiples scripts a la vez. Por ejemplo, --script=http-* ejecutará todos los scripts relacionados con el protocolo HTTP. El uso de scripts puede aumentar significativamente la eficacia de un escaneo de Nmap, ya que permite a los usuarios detectar vulnerabilidades y recopilar información que de otra manera sería difícil de obtener.

# Scripts
- `Script Auth`: Este parámetro ejecuta solo scripts de autenticación. Estos scripts están diseñados para identificar y verificar la autenticación en servicios de red que requieren credenciales para el acceso.
- `Script Default`: Al utilizar este parámetro, Nmap ejecutará los scripts predeterminados que considera seguros y útiles en la mayoría de los casos. Estos scripts cubren una amplia gama de funcionalidades y son una opción equilibrada para escaneos generales.
- `Script Safe`: Similar al parámetro "Default", este ejecuta solo scripts que son considerados seguros y no intrusivos. Es útil cuando se desea evitar la ejecución de scripts más agresivos que podrían afectar la estabilidad o la seguridad de los sistemas objetivo.
- `Script Vuln`: Este parámetro ejecuta scripts específicamente diseñados para detectar vulnerabilidades en los sistemas objetivo. Son útiles para realizar evaluaciones de seguridad más detalladas y encontrar posibles puntos de entrada para ataques.
- `Script Discovery`: Recupera información del target o víctima
- `Script All`: Como su nombre indica, este parámetro ejecuta todos los scripts disponibles en la biblioteca de Nmap. Puede ser útil para una evaluación exhaustiva de la seguridad, pero también puede aumentar significativamente el tiempo de escaneo y generar más tráfico en la red, lo que podría llamar la atención no deseada.

Ejemplo: 
```
nmap --script vuln <target>
```


-----------------------------

# Ruta Nmap Scripting engine (NSE)
La ruta donde se ubican los scripts de nmap
`/usr/share/nmap/scripts`

# Añadir argumento a script
`--script-args`
Ejemplo:
```
nmap -sV -p 80 --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi" <IP>
```

# Obtener información de script sobre un protocolo
Para realizar una busqueda exacta sobre un protocolo podemos utilizar el siguiente comando
ls -la /usr/share/nmap/scripts | grep -e "protocolo"
ls -la /usr/share/nmap/scripts | grep "smb"
![[Pasted image 20240304100441.png]]

# Descubrir funcionamiento de los scripts
Para obtener mas información sobre un scrip y saber si es intrusivo o no podemos utilizar el siguiente comando
nmap --script-help='script_a_preguntar'
nmap --script-help smb-security-mode
![[Pasted image 20240304101140.png]]

# Ejecutar scripts predeterminados
Para ejecutar los script predeterminados de nmap añadiremos el siguiente parametro -sC, es importante añadir el escaneo de puertos para que pueda ser valido el escaneo.
```
nmap -sS -sV -sC -p- -T4 [IP]
```

# Ejecutar script concreto
Para ejecutar un script en particulas escribiremos el siguiente comando
```
nmap -sS -sV --script='nombre del script' -p- -T4 [IP]
nmap -p445 --script smb-security-mode 10.4.31.137
```
![[Pasted image 20240304100658.png]]

# Ejecutar todos los scripts de un protocolo
Utilizando el * podemos ejecutar todos los scripts de un protocolo en concreto
```
nmap -sS -sV --script ftp-* -p55413 -T4
nmap -p445 --script smb* -T4 10.4.31.137
```
![[Pasted image 20240304101216.png]]

# SCRIPT PARA HACER FUZZING
Podemos hacer fuzzing con un script de nmap, donde vamos a hacerlo sobre el puerto 80 de la [[MAQUINA OVERPASS (Obtener id_rsa modificando cookies en web, ssh2john para cracking de ir_rsa y escalada privilegios permisos suid con exploit de pkexec)]] de tryhackme para detectar directorios web:
```bash
nmap --script http-enum -p80 10.10.186.249 -vvv
```
![[Mis apuntes/ANEXOS/Pasted image 20230501191549.png]]

### SCRIPT VULN PARA DETECTAR VULNERABILIDADES
Podemos mirar si esta máquina [[MAQUINA BLUE (Explotación vulnerabilidad blue)]] de tryhackme es vulnerable a alguna vulnerabilidad; y vemos que sí lo es a eternalblue:
![[Mis apuntes/ANEXOS/Pasted image 20230427115145.png]]

Por tanto vamos a usar metasploit para ganar acceso al sistema explotando esta vulnerabilidad utilizando el siguiente exploit:
![[Mis apuntes/ANEXOS/Pasted image 20230427120812.png]]

Realizamos las configuraciones básicas:
![[Mis apuntes/ANEXOS/Pasted image 20230427120834.png]]

Configuramos el payload correspondiente, ya que el que viene por defecto da error:
![[Mis apuntes/ANEXOS/Pasted image 20230427120914.png]]

Y si ejecutamos el comando run ya estaríamos dentro:
![[Mis apuntes/ANEXOS/Pasted image 20230427120933.png]]
# SCRIPT DE NMAP PARA ATAQUES DE FUERZA BRUTA SSH
Para hacer un ataque de fuerza bruta al puerto ssh, podemos hacerlo con el siguiente parámetro de nmap:
```bash
nmap --script ssh-brute 192.168.0.25
```

Y nos realiza el ataque probando usuarios y contraseñas:
![[Mis apuntes/ANEXOS/Pasted image 20230501193242.png]]

Pero en caso de conocer el nombre de usuario, que por ejemplo es mario, y querer encontrar sólo la contraseña, lo haríamos de la siguiente forma:
```bash
nmap -p 22 --script ssh-brute --script-args userdb='usuario.txt',passdb='rockyou.txt' 192.168.0.25
```

Y vemos que ahora comprueba las distintas contraseñas para el usuario mario:
![[Mis apuntes/ANEXOS/Pasted image 20230501194124.png]]
# SCRIPT ENUMERAR SMB
Podemos usar este script para ver vulnerabilidades de smb:
```bash
nmap -p445 --script smb-protocols 192.168.0.48
```
![[Mis apuntes/ANEXOS/Pasted image 20230727142007.png]]

También podemos saber la seguridad si permite iniciar sesión como invitado o no con este otro script, de tal forma que podríamos entrar sin proporcionar contraseña:
```bash
nmap -p445 --script smb-security-mode 192.168.0.48
```
![[Mis apuntes/ANEXOS/Pasted image 20230727142202.png]]

# LISTAR RECURSOS COMPARTIDOS SMB
Podemos también listar recursos compartidos con nmap usando el siguiente script:
```bash
nmap -p445 --script smb-enum-shares 192.168.0.48
```
![[Mis apuntes/ANEXOS/Pasted image 20230727150238.png]]

# Script enumerar baner
El script de banner enumera la versión que utiliza los sistemas y puertos
```
nmap -sV -- script=banner 192.8.94.3
```
![[Pasted image 20240416075533.png]]