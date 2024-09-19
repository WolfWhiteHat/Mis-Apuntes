# Descargar Ventoy

Kali linux-live
https://www.kali.org/get-kali/#kali-live

Ubunutu
https://ubuntu.com/download/desktop/thank-you?version=23.10.1&architecture=amd64

Descargar ventoy
https://github.com/ventoy/Ventoy/releases/

Versiones ventoy
[https://www.ventoy.net/en/download.html](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa19veWlydlRKQjc3d3VuUXRmQS10ZG9iR0UxZ3xBQ3Jtc0trNkYxQmRpZVJoWG9nSUlrRmM1b0FqSEFUeTNIN2VWVVB4eDg4ZW1rYVlnUnBKZHVFVUc2NzU2WnRJallDRzlOdmZudjhBdGItRU9iUnpNU0lJT1FDZi1XZEpINGViVEN4aXJFb0RLakxYRVFPYl9Wbw&q=https%3A%2F%2Fwww.ventoy.net%2Fen%2Fdownload.html&v=rxctTc1xwSo)

Descomprimir Ventoy
![[Captura de pantalla 2023-11-08 a las 8.27.57.png]]

Mover ventoy
![[Pasted image 20231108084009.png]]

Comprobar unidades de almacenamiento 
![[Pasted image 20231108084453.png]]

Con el siguiente comando instalaremos ventoy
![[Pasted image 20231108085244.png]]
-I para forzar la instalación y -s para habilitar el soporte de secure boot

Comprobamos que este instalado correctamente en nuestro USB
![[Pasted image 20231108085426.png]]


# Crear USB persistente
Ejecutar scrip para crear archivo persistente
![[Pasted image 20231108090050.png]]
Con el parametro -s 4096 creamos el archivo persistente y le indicamos el tamaño, en este caso 4G

Verificamos que el archivo persistente se ha creado correctamente
![[Captura de pantalla 2023-11-08 a las 9.04.11.png]]

Comprobar nombre USB
![[Captura de pantalla 2023-11-08 a las 9.16.01.png]]

Movemos el archivo persistencia a ruta USB
![[Pasted image 20231108092020.png]]

Ahora vamos a crear una carpeta para alojar una archivo json para indicarle que nuestrar isos sean persistentes.
![[Captura de pantalla 2023-11-08 a las 9.28.12.png]]

Ventoy.json configurado
![[Pasted image 20231108104249.png]]
{
  "persistence": [
    {
      "image": "/kali-linux-2023.3-live-amd64.iso",
      "backend": "/persistence.dat"
    },
    {
      "image": "/ubuntu-23.10.1-desktop-amd64.iso",
      "backend": "/persistence1.dat"
    }
  ]
}
Si queremos tener mas de un sistema con persistencia crearemos otro archivos persistente, con los siguientes comandos creamos un segundo archivo, lo ubicamos en nuestra carpeta de ventoy del USB y le cambiamos el nombre
![[Pasted image 20231108093253.png]]


# Tutorial Ventoy

https://www.youtube.com/watch?v=rxctTc1xwSo