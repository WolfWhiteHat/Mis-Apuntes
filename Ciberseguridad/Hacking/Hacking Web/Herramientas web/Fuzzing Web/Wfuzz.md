Esta herramienta sirve para fuzzear todo tipo de parámetro, incluso para encontrar subdominios [[Detectar subdominios]].

# Fuzzing directorios ocultos
Para buscar directorios ocultos, lo haremos con este comando y utilizando uno de los diccionarios que se encuentran en la ruta /usr/share/wordlists/dirbuster:
```python
wfuzz -c --hc 404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt https://google.es/FUZZ
```

- `-c`: Este parámetro indica que la herramienta debe mostrar el resultado de las peticiones que devuelvan un código de estado HTTP diferente a 404 (es decir, mostrar solo las páginas encontradas).
- `--hc 404`: Indica que las respuestas HTTP con un código de estado 404 (no encontrado) deben ser tratadas como válidas y no deben mostrarse como resultados.
- `-t 200`: Especifica el tiempo de espera máximo por cada solicitud en milisegundos (200 milisegundos en este caso). Esto controla cuánto tiempo espera `wfuzz` para recibir una respuesta antes de considerar que la solicitud ha fallado.

Y nos encuentra dos directorios ocultos:
![[Mis apuntes/ANEXOS/Pasted image 20230210132331.png]]

# Fuzzing de extensiones de archivos
Si queremos fuzzear por extensiones de archivos, lo haremos de la siguiente forma:
```python
wfuzz -c --hc 404 -w diccionario.txt http://example.com/FUZZ.php
```

# Fuzzing de subdominios
Podemos detectar subdominios con wfuzz de la siguiente forma:
```bash
wfuzz -c --hc=404,200 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -H "Host: FUZZ.hunterzone.nyx" -u 192.168.0.40
```

 - `--hc=404,200`: Considerará como válidas las respuestas HTTP que tengan un código de estado 404 (no encontrado) o 200 (éxito). Esto puede ser útil si se busca identificar recursos existentes o no en el servidor.
- `-H "Host: FUZZ.hunterzone.nyx"`: Especificar un encabezado HTTP personalizado (`Host`). El valor de `Host` se establece como `FUZZ.hunterzone.nyx`, donde `FUZZ` es un marcador de posición que `wfuzz` reemplazará con cada palabra de la lista de palabras.
- `-u`: Especifica la url a escanear

# FUERZA BRUTA PANEL DE LOGIN CON WFUZZ
También podemos hacer un ataque de diccionario con wfuzz para probar muchos posibles usuarios dentro de un panel de login, por ejemplo en una web donde si pongo un usuario, me dice si existe o no en el sistema como en este caso:
![[Mis apuntes/ANEXOS/Pasted image 20230210132724.png]]

Por tanto yo puedo probar con muchos usuarios a ver si en alguno me dice que sí existe este usuario. Utilizando este diccionario, con WFUZZ podemos hacer estas comprobación de esta forma:
![[Mis apuntes/ANEXOS/Pasted image 20230210133127.png]]

Pero así lo que ocurre es que me muestra cada uno de los intentos:
![[Mis apuntes/ANEXOS/Pasted image 20230210133435.png]]

Pero con wfuzz, podemos decir que siempre y cuando el mensaje de error de la web sea el mismo, que no lo muestre; y que sólo nos muestre el usuario que genera un mensaje diferente en la web; usando el parámetro --hs:
![[Mis apuntes/ANEXOS/Pasted image 20230210133523.png]]

Y nos encuentra el usuario Tyler:
![[Mis apuntes/ANEXOS/Pasted image 20230210133537.png]]

[[MAQUINA SECNOTES (SQL Injection, CSRF (Cross-site request forgery), detectar usuarios válidos con wfuzz, netcat en windows, php malicioso y escalar privilegios en máquina Windows con subsistema de Linux instalado a través de ejecutar un bash.exe)]]



