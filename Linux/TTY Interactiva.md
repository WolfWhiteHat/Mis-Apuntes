Primero tenemos que obtener acceso a la maquina
![[Pasted image 20240602122839.png]]

Una vez tenemos acceso ejecutamos el siguiente comando
```Bash
script /dev/null -c bash
```
![[Pasted image 20240602122945.png]]

Ahora suspendemos la sesion con CNTRL + Z
![[Pasted image 20240602123029.png]]

Ahora resetearemos la configuración de la shell que dejamos en segundo plano indicando **reset** y **xterm**, para ello primero ejecutamos el siguiente comando
```Bash
stty raw -echo; fg
```
![[Pasted image 20240602123255.png]]

Una vez ejecutado y como aparece en la siguiente imagen escribimos reset y posteriormente xterm
![[Pasted image 20240602123410.png]]

Exportamos las siguientes variables
```Bash
export TERM=xterm
export SHELL=bash
```
- `export TERM=xterm` -> Debemos hacer esto ya que a pesar de haberle indicado que queríamos una **xterm** al momento de reiniciarlo la variable de entorno **TERM** vale **dump** (Se usa esta variable para poder usar los atajos de teclado).
- `export SHELL=bash` -> Para que nuestra shell sea una bash.
![[Pasted image 20240602123456.png]]

Ya con esto hecho tendríamos una **TTY** full interactiva, pero falta una cosa para que sea lo más comoda posible, setear las filas y columnas, esto para poder ocupar toda nuestra pantalla ya que en este momento solo podemos usar una porción de esta
Vemos el tamaño de nuestra shell en pantalla
```Bash
stty size
```
![[Pasted image 20240602123816.png]]

Y las seteamos en la reverse shell
```Bash
stty rows 40 columns 123
```
![[Pasted image 20240602123910.png]]


