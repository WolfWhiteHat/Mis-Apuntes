Bspwm (Binary Space Partitioning Window Manager) es un administrador de ventanas para el sistema X Window System en sistemas Unix y similares a Unix. A diferencia de otros administradores de ventanas, bspwm no gestiona las ventanas a través de un bucle de eventos interno; en su lugar, lo hace respondiendo a mensajes enviados desde un programa externo llamado `bspc`.

```
https://github.com/baskerville/bspwm
```

```
https://s4vitar.github.io/bspwm-configuration-files/#
```

# Instalación bspwm

```Bash
apt-get install bspwm
```
![[Pasted image 20240611073226.png]]

Comprobamos que esta instaldo
![[Pasted image 20240611073248.png]]

Instalamos las siguientes dependencias con este comando:
```Bash
sudo apt-get install libxcb-xinerama0-dev libxcb-icccm4-dev libxcb-randr0-dev libxcb-util0-dev libxcb-ewmh-dev libxcb-keysyms1-dev libxcb-shape0-dev
```

Ahora ejecutamos los siguientes comandos
```
git clone https://github.com/baskerville/bspwm.git
git clone https://github.com/baskerville/sxhkd.git
cd bspwm && make && sudo make install
cd ../sxhkd && make && sudo make install
```


Ahora ejecutamos los siguientes comandos:
```Bash
mkdir -p ~/.config/{bspwm,sxhkd}
cp /usr/share/doc/bspwm/examples/bspwmrc ~/.config/bspwm/
cp /usr/share/doc/bspwm/examples/sxhkdrc ~/.config/sxhkd/
chmod u+x ~/.config/bspwm/bspwmrc
```
![[Pasted image 20240611084723.png|250]]

Una vez terminado creamos el siguiente archivo `.xinitrc` y le agreamos la siguiente configuración
```Bash
nano ~/.xinitrc
```
![[Pasted image 20240611085004.png]]

Continuamos descargandonos compton y feh para gestionar los fondos de pantalla
```Bash
apt-get install compton feh -y
```
![[Pasted image 20240611085114.png]]

Abrimos un editor para modificar el archivo `bspwmrc` el cual es un script de inicio para el gestor de ventanas bspwm
```Bash
nano ~/.config/bspwm/bspwmrc
```
![[Pasted image 20240611085900.png]]

Ahora abriremos el siguiente archivo para configurar los atajos de teclados del programa `sxhkd`
```Bash
nano ~/.config/sxhkd/sxhkdrc
```
![[Pasted image 20240611091337.png]]

Ahora instalaremos rofi
```Bash
apt-get install rofi
```
![[Pasted image 20240611090408.png]]

Ahora configuramos el archivo sxhkdrc al completo como mas nos guste y creamos un directorio y un archivo que contiene un script
```Bash
mkdir /home/kali/.config/bspwm/scripts/
nano /home/kali/.config/bspwm/scripts/bspwm_resize
```
![[Pasted image 20240611092223.png]]

Y agregamos permisos de ejecución al script
![[Pasted image 20240611093941.png]]

Una vez hecho esto ejecutando el siguiente comando se cierra la sesión y tendremos que seleccionar la pestaña de bspwm
```
kill -9 -1
```

Una vez dentro del terminal para cambiar la el menu de rofi ejecutamos le siguiente comando
```
rofi-theme-selector
```
![[Pasted image 20240611102915.png]]


https://www.youtube.com/watch?v=66IAhBI0bCM