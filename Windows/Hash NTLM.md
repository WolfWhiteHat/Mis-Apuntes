Tenemos el siguiente hash extraido de un sistema Windows
```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::
```
![[Pasted image 20240722120221.png]]
- **Username**: `Administrator` - Este es el nombre del usuario de la cuenta. En este caso, corresponde a la cuenta del administrador del sistema.
- **User ID (UID)**: `500` - Este es el identificador único del usuario dentro del sistema. El UID `500` está típicamente asignado al administrador del sistema en Windows.
- **LM hash**: `aad3b435b51404eeaad3b435b51404ee` - Este es el hash LM (LAN Manager) de la contraseña del usuario. El LM hash es una forma antigua y menos segura de almacenar contraseñas. Es conocido por ser vulnerable a ataques de fuerza bruta y otras técnicas de cracking debido a su estructura débil (se divide la contraseña en dos bloques de 7 caracteres y se hash cada uno por separado).
- **NTLM hash**: `fc525c9683e8fe067095ba2ddc971889` - Este es el hash NTLM de la contraseña del usuario. NTLM (NT LAN Manager) es una versión más segura que el LM hash y es el método estándar en versiones más recientes de Windows. Sin embargo, sigue siendo susceptible a ciertos tipos de ataques criptográficos, especialmente si la contraseña es débil.
- **Los campos vacíos al final**: Estos son a menudo reservados para el uso de ciertos valores como el directorio home del usuario, la contraseña expirada, etc., pero en este caso están vacíos.

