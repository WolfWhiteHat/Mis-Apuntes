"Pass-the-hash" es una técnica utilizada en ataques informáticos para comprometer la seguridad de un sistema y obtener acceso no autorizado a recursos protegidos. Esta técnica se basa en el robo y el uso de hashes de contraseñas en lugar de las contraseñas reales.

Aquí está el proceso básico de cómo funciona "pass-the-hash":

1. **Obtención del hash de la contraseña**: El atacante primero debe obtener el hash de la contraseña de un usuario legítimo. Esto puede lograrse mediante el uso de herramientas de hacking que extraen hashes almacenados localmente en un sistema comprometido o mediante ataques de ingeniería social, phishing u otras técnicas de ingeniería social para obtener acceso a los hashes de contraseñas.
    
2. **Uso del hash**: Una vez que el atacante tiene el hash de la contraseña, puede utilizarlo directamente en lugar de la contraseña real para autenticarse en el sistema comprometido o acceder a otros recursos protegidos. En lugar de enviar la contraseña en texto plano, el atacante envía el hash de la contraseña al sistema, que luego lo compara con el hash almacenado en su base de datos. Si los hashes coinciden, se permite el acceso.
    
3. **Movimiento lateral**: Una vez que el atacante ha obtenido acceso a un sistema utilizando "pass-the-hash", puede utilizar esa posición para moverse lateralmente a través de la red, escalando privilegios y accediendo a otros sistemas y recursos.


### Practica

Aqui tenemos el hash de LM
![[Pasted image 20240312082121.png]]


Habiendo obtenido el hash de un usuario configuraremos y ejecutaremos el siguiente exploit
![[Pasted image 20240312082313.png]]
![[Pasted image 20240312082656.png]]
![[Pasted image 20240312082720.png]]

Como podemos ver hemos obtenido una sesion con el usuario administrador y su hash
![[Pasted image 20240312082812.png]]

![[Pasted image 20240312082836.png]]



