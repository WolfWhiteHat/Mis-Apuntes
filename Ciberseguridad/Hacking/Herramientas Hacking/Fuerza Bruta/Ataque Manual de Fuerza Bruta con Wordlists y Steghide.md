Con el siguiente script podriamos realizar el ataque de fuerza bruta con steguide
```Bash
#!/bin/bash

# Archivo a atacar
archivo="archivo_oculto.jpg"
# Wordlist
wordlist="ruta/a/tu/wordlist.txt"

# Iterar sobre las contraseñas en la wordlist
while read -r password; do
  echo "Probando contraseña: $password"
  
  # Intentar extraer los metadatos con StegHide
  steghide extract -sf "$archivo" -p "$password" -f
  if [ $? -eq 0 ]; then
    echo "Contraseña encontrada: $password"
    break
  fi
done < "$wordlist"
```

Ahora modificamos las variables de `archivo` y `wordlist` con el fichero a crackear y el diccionario
