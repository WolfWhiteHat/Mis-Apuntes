TestDisk es una herramienta de software de código abierto diseñada principalmente para ayudar en la recuperación de datos perdidos en discos duros y para hacer que los discos dañados sean nuevamente booteables. Fue creada para ser utilizada en sistemas operativos como Linux, Windows y macOS. TestDisk es parte del conjunto de herramientas de recuperación de datos de la suite TestDisk & PhotoRec.

Primero abrimos la carpeta de la herramienta y crearemos una ruta para poder guardar los resultados, después ejecutamos el programa
![[Captura de pantalla 2024-04-05 a las 12.29.58.png]]

Seleccionamos `Create`

Especificamos el disco a analizar
![[Pasted image 20240405123142.png]]

Seleccionamos el sistema a escanear, en nuestro caso es Windows
![[Pasted image 20240405123218.png]]

Seleccionamos `Advanced`
![[Pasted image 20240405124109.png]]

Seleccionamos la aprticion y aabajo tenemos las opciones, seleccionaremos

![[Pasted image 20240405124140.png]]
1. `Type`: Esta opción te permite cambiar el tipo de partición. Por ejemplo, puedes cambiar una partición de tipo NTFS a FAT32 o viceversa.
2. `Boot`: Con esta opción puedes cambiar el estado de arranque de una partición. Esto es útil si tienes problemas para iniciar desde una partición específica.
3. `List`: Esta opción te permite listar los archivos y directorios dentro de una partición seleccionada. Es útil para verificar la integridad de los datos y para identificar qué archivos están presentes en la partición.
4. `Undelete`: Esta opción te permite recuperar archivos eliminados de una partición. TestDisk intentará restaurar los archivos eliminados y devolverlos a su estado original.
5. `Image Creation`: Con esta opción puedes crear una imagen de la partición seleccionada. Esto puede ser útil como una medida de seguridad para respaldar datos antes de realizar operaciones de recuperación o reparación.
6. `Quit`: Esta opción te permite salir de TestDisk y volver al sistema operativo normal.



https://www.softzone.es/programas/sistema/testdisk/