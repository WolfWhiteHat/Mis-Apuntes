Steghide es una herramienta de software utilizada para la esteganografía, que es la práctica de ocultar mensajes u otra información dentro de otros archivos para evitar la detección. En particular, Steghide permite ocultar datos dentro de varios tipos de archivos multimedia, como imágenes, archivos de audio y otros formatos. La herramienta no solo oculta los datos, sino que también encripta el contenido oculto para proporcionar una capa adicional de seguridad.

# Instalación Steghide
```Bash
apt-get install steghide
```


# Obtener información de un archivo
```Bash
steghide info Alice-White-Rabbit.jpg
```
![[Pasted image 20240530110148.png]]

# Extraer información
```Bash
steghide extract -sf Alice-White-Rabbit.jpg
```
![[Pasted image 20240530110240.png]]

# Insertar datos
```Bash
steghide embed -cf <archivo> -ef secret.txt
```