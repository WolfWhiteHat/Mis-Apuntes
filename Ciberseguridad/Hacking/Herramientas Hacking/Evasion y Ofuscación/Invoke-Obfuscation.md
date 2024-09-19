Es una herramienta de seguridad informática utilizada para ofuscar y ofuscar scripts de PowerShell. La herramienta permite a los usuarios modificar y ofuscar scripts de PowerShell de diversas maneras, esto puede incluir la alteración de nombres de variables, funciones y cmdlets, así como la introducción de técnicas de codificación y cifrado para dificultar aún más la detección.
https://github.com/danielbohannon/Invoke-Obfuscation

# Instalación de invoke-Obfuscation
```
wget https://github.com/danielbohannon/Invoke-Obfuscation.git
```

Una vez instalado la herramienta necesitaremos instalar las dependencias de PowerShell para poder ejecutarlo en Linux
```
sudo apt-get install powershell -y
```
![[Pasted image 20240503123450.png]]

Ahora para ejecutar powershell en linux unicamente tendremos que ejecutar el siguiente comando y obtendremos una sesion de powershell en linux
```
pwsh
```
![[Pasted image 20240503123554.png]]

Una vez dentro de la sesion de powershell accedemos a la carpeta de la herramienta de invoke-Obfuscation y listamos todas las opciones que tenemos
![[Pasted image 20240503123748.png]]

Ahora ejecutamos el siguiente comando para importar el modulo 1
```
Import-Module ./Invoke-Obfuscation.psd1
```
![[Pasted image 20240503123928.png]]

Invocamos el programa y ya accederemos para poder ofuscar nuestro codigo de powershell
```
Invoke-Obfuscation
```
![[Pasted image 20240503124127.png]]

Ahora crearemos el script, de este codigo unicamente necesitamos cambiar la ip por la nuestra y el puerto que queramos configurar y lo guardamos en formato ps1
![[Pasted image 20240503124439.png]]

Ahora estando en el menu de invoke seleccionaremos el script que queramos ofuscar, en la siguiente imagen podemos ver el menu y las opciones que tenemos
![[Pasted image 20240503124712.png]]

Ahora seleccionamos el script
```
SET SCRIPTPATH /home/kali/Desktop/AVBypass/shell.ps1
```
![[Pasted image 20240503124831.png]]

Seleccionamos la opción que mas se adecue segun el sistema o lo que queremos hacer, en este caso seleccionaremos AST
![[Pasted image 20240503125457.png]]

Ahora seleccionaremos la opción ALL
![[Pasted image 20240503125614.png]]

Seleccionamos la opción 1 y ya nos mostrara el codigo ofuscado
![[Pasted image 20240503125727.png]]

Copiamos el codigo y lo pegamos en un bloc de notas, como podemos ver es diferente al original
`Codigo ofuscado`
![[Pasted image 20240503125810.png]]

`Codigo original`
![[Pasted image 20240503125847.png]]

Ahora solo faltaria ejecutarlo en la maquina windows victima, para ello cargaremos netcat y un servidor para enviar el archivo
![[Pasted image 20240503130012.png]]


Ejecutamos el script en la maquina de windows 10
![[Pasted image 20240503130158.png]]

Como podemos ver a abierto la pestaña de powershell, eso significa que hemos evadido el sistema de antivirus de windows
![[Pasted image 20240503130230.png]]

Como podemos ver ya hemos obtenido una reverse shell
![[Pasted image 20240503130418.png]]

