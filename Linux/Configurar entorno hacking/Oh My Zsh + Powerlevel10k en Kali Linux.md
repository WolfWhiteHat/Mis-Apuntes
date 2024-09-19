# Configuración fondo y teclado
![[Pasted image 20240607114825.png|500]]

# Instalar Oh My Zsh
```
`sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
```
![[Pasted image 20240607115608.png]]

# Instalar Powerleverl10
Clonamos el repositorio
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
![[Pasted image 20240607115640.png]]


Una vez copiado el repositorios modicifaremos el fichero `zshrc` el cual sirve para configurar y personalizar nuestra shell y añadimo el siguiente contenido a `ZSH_THEME`
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```
![[Pasted image 20240607115834.png]]
![[Pasted image 20240607121150.png]]

Y ahora vamos a aplicar los cambios
![[Pasted image 20240607120052.png]]

Una vez lo ejecutemos se nos abrira el menu para configurarlo
![[Pasted image 20240607121232.png]]

Una vez elegidas las opciones al terminal ya tendriamos configurada la nueva terminal
![[Pasted image 20240607122112.png]]

Si ahora queremos voler a configurar la terminal podriamos hacerlo ejecutando el siguiente comando
```Bash
p10kconfigure
```

Ahora vamos a recuperar la posibilidad de que nuestra zsh pueda detectar los comandos y nos los marque, tendriamos que instalar este pluging, como lo estamos configurando en kali linux ya viene preinstalado, como podemos ver al internar instalarlo nos indica que ya lo tenemos instalado
```
https://github.com/zsh-users/zsh-syntax-highlighting/tree/master
```
```
sudo apt install zsh-syntax-highlighthing
```
![[Pasted image 20240607122704.png]]

Para activarlo tenemos que añadir la siguinte linea a la configuración del fichero `zshrc`
```Bash
echo "source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> /home/kali/.zshrc
```
![[Pasted image 20240607123244.png]]

El comando de abajo muestra cada segundo la modificación final del archivi, si quisieramos mostrar el principio cambiariamos tails por less
```bash
watch -n 1 "tail /home/wolf/.zshrc"
```

Ahora añadiremos un pluging mas para que nos muestre sugerencias de comandos que ya hemos ejecutado, para ello añadimos la siguiente linea al fichero `.zshrc`
```Bash
echo "source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> /home/kali/.zshrc
```
![[Pasted image 20240607123631.png]]

Ahora solo quedaria reiniciar el archivo .zshrc
![[Pasted image 20240607123815.png]]