Realizamos un escaneo de nmap y encontramos el puerto 80 abierto
![[Pasted image 20240627135939.png]]

Al acceder a la web encontramos lo sigueinte
![[Pasted image 20240627140022.png]]

Parecen ser unas puertas, si hacemos curl podemos ver que es una imagen en la cual tiene cordenadas en md5
![[Pasted image 20240627140154.png]]
![[Pasted image 20240627140131.png]]
![[Pasted image 20240627142153.png]]
```
c4ca4238a0b923820dcc509a6f75849b
c81e728d9d4c2f636f067f89cc14862c
eccbc87e4b5ce2fe28308fd9f2a7baf3
a87ff679a2f3e71d9181a67b7542122c
e4da3b7fbbce2345d7772b0674a318d5
1679091c5a880faf6fb5e6087eb1b2dc
8f14e45fceea167a5a36dedd4bea2543
c9f0f895fb98ab9159f51fd0297e236d
45c48cce2e2d7fbdea1afc51c7c6ad26
d3d9446802a44259755d38e6d163e820
6512bd43d9caa6e02c990b0a82652dca
c20ad4d76fe97759aa27a0c99bff6710
c51ce410c124a10e0db5e4b97fc2af39
```

Si accedemos a una de las puertas entramos a otro directorio
![[Pasted image 20240627140412.png]]

Ahora probaremos a crackear todos los hashes y los conseguimos crackear todos
![[Pasted image 20240627142446.png]]


Ahora crearemos un script para sacar los hashes en cadena para encontrar mas directorios
```Python
import hashlib
import sys

def usage():
    print(f'python3 {sys.argv[0]} <text_to_hash>')
    exit()

def create_hash(t):
    md5hash = hashlib.md5(t.encode()).hexdigest()
    print(md5hash)

if len(sys.argv) != 2:
    usage()

create_hash(sys.argv[1])
```
![[Pasted image 20240627144824.png]]

El script hace lo siguiente:
- **Función `usage`**: Imprime cómo usar el script y sale si el número de argumentos no es correcto.
- **Función `create_hash`**: Genera y imprime el hash MD5 del texto proporcionado.
- **Argumentos de línea de comandos**: Verifica que se ha proporcionado exactamente un argumento. Si no, llama a `usage`.
- **Generación del hash**: Llama a `create_hash` con el argumento proporcionado para generar el hash MD5.

Ejecutamos el script con los parametros y obtenenemos el hash
![[Pasted image 20240627144916.png]]

Ahora vamos al navegador y al escribirlo obtenemos la flag
![[Pasted image 20240627144944.png]]