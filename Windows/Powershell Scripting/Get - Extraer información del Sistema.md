Hay varios comandos con get que nos sirven para extraer distinto tipo de información.

PARA CONOCER EL HOST:

![[Mis apuntes/ANEXOS/Pasted image 20221217104021.png]]

PARA CONOCER EL PATH ACTUAL DE TRABAJO:

![[Mis apuntes/ANEXOS/Pasted image 20221217104028.png]]
PARA VER LOS PROCESOS QUE SE ESTÁN EJECUTANDO EN EL SISTEMA:

![[Mis apuntes/ANEXOS/Pasted image 20221217104036.png]]
PARA VER LA FECHA ACTUAL:

![[Mis apuntes/ANEXOS/Pasted image 20221217104043.png]]

### EXTRAER CONTENIDO DE UN ARCHIVO

Por ejemplo, si quiero visualizar el contenido de un archivo y aplicar una tubería para que me busque algo, lo haría de esta forma:
```powershell
Get-Content direcciones_ip.txt | Select-String -Pattern "192"
```
![[Mis apuntes/ANEXOS/Pasted image 20230509151233.png]]


