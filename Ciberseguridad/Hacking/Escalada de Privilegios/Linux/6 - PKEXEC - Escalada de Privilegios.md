En caso de encontrarnos con el binario SUID de pkexec, podemos escalar privilegios de esta forma:
![[Mis apuntes/ANEXOS/Pasted image 20230507113855.png]]

Por lo que buscamos un exploit para explotar esta vulnerabilidad y lo ejecutamos en la máquina víctima:
```
https://github.com/Almorabea/pkexec-exploit
```
![[Mis apuntes/ANEXOS/Pasted image 20230507113929.png]]

Lo compartimos con la máquina víctima, lo ejecutamos y ya somos root:
![[Mis apuntes/ANEXOS/Pasted image 20230507114002.png]]


Esta vulnerabilidad esta corregida de la version 0.105 en adelante
![[Pasted image 20240606080350.png]]