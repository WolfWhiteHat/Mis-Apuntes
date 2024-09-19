Lo primero será estar dentro de una máquina windows con un meterpreter y siendo usuario administrador:
![[Mis apuntes/ANEXOS/Pasted image 20230801122738.png]]
Una vez hecho esto, usaremos el siguiente módulo, poniendo la sesión en segundo plano y luego volviendo a cargarla:
```bash
use exploit/windows/local/persistence_service
```
![[Mis apuntes/ANEXOS/Pasted image 20230801122857.png]]
Ahora, por otra parte, nos ponemos a la escucha con metasploit para recibir una nueva conexión en caso de reiniciar la máquina:
![[Mis apuntes/ANEXOS/Pasted image 20230801123340.png]]
Apagamos la máquina víctima:
![[Mis apuntes/ANEXOS/Pasted image 20230801123445.png]]
Pero en la otra ventana de metasploit habremos recibido la conexión una vez que la máquina víctima se haya reiniciado:
![[Mis apuntes/ANEXOS/Pasted image 20230801123520.png]]
