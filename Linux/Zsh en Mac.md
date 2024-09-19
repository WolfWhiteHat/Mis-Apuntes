# Instalar ZSH
```Bash
sudo apt install zsh
```


# Instalar Oh-My-Zsh
```Bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


# Cambiar de bash a zsh
```Bash
chsh -s /bin/zsh
```

# Cambiar de zsh a Bash
```Bash
chsh -s /bin/bash
```


# Añadir temas a zsh

Primero clonaremos el repositorio de github que queramos instalar
```Bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

Después accedemos al directorio de `~/.oh-my-zsh/themes` y en la carpeta de temas subiremos el fichero clonado de github
```
cp -r powerlevel10k /ruta/.oh-my-zsh/themes/
```
![[Pasted image 20240918112501.png]]
![[Pasted image 20240918112625.png]]

Ahora modificamos el fichero `~/.zshrc` y en la fila donde este `ZSH_THEME` añadimos `ZSH_THEME="powerlevel10k/powerlevel10k"`
![[Pasted image 20240918112742.png]]
![[Pasted image 20240513143737.png]]

Una vez realizados los cambios para aplicarlos tendremos que reiniciar el terminal o ejecutar el siguiente comando
```Bash
source ~/.zshrc
```

Una vez realizado esto ya estariamos ejecutando un terminal de zsh
![[Pasted image 20240513144026.png]]


# Añadir plugins
Para añadir plugins primero tendremos que instalarnos el repositorio y añadirlo a la ruta `~/.oh-my-zsh/plugins`
![[Pasted image 20240918112840.png]]

Una vez añadido iremos al archivo `~/.zshrc` y en el apartado de plugins incluiremos el plugins que hayamos añadido
![[Pasted image 20240513145346.png]]

# Bibliografia

[https://ohmyz.sh/](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqazQtWFFIWXl0d1A4MVpXaV9MbndmOFNfdkNyZ3xBQ3Jtc0trRVZ5Z0V2T19rN1VIR3Ftb2dQSWtweEZUSnVTQXVoYVdrV2RJcVVjc3BnUWF0QlVqWEZzTThxOXgycWdZZFQ0dE5vNjhqVUJrVWFBZmZVUlJQY3JlbXZMVUVsbm03V2dqaXFjb2UyLWlmOGYtMUVvMA&q=https%3A%2F%2Fohmyz.sh%2F&v=35EN3iP1-8c)
https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins
https://github.com/romkatv/powerlevel10k

# Tutorial
https://www.youtube.com/watch?v=35EN3iP1-8c