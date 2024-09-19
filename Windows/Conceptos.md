# LSASS
  
LSASS, o Local Security Authority Subsystem Service, es un proceso en el sistema operativo Windows que maneja la autenticación de usuarios, la política de seguridad y la gestión de credenciales de inicio de sesión. Es esencial para el funcionamiento seguro del sistema operativo Windows. LSASS es responsable de procesar las solicitudes de inicio de sesión, autenticar usuarios para permitirles acceder a recursos del sistema y aplicar políticas de seguridad, como restricciones de acceso y contraseñas. Además, también gestiona la creación y validación de tokens de seguridad para los usuarios y procesos del sistema. Debido a su importancia crítica para la seguridad del sistema, LSASS está protegido por el mecanismo de protección de integridad de seguridad de Windows y se ejecuta en un proceso con privilegios elevados.

# SAM
SAM, que significa "Security Account Manager" (Administrador de Cuentas de Seguridad), es una parte fundamental del sistema operativo Windows. SAM almacena información sobre las cuentas de usuario en el sistema, incluidos nombres de usuario y contraseñas hash. Este almacén de datos es esencial para la autenticación de usuarios durante el proceso de inicio de sesión.

En el contexto de sistemas operativos Windows, SAM es un archivo o base de datos que reside típicamente en el directorio %SystemRoot%\System32\Config. Este archivo SAM está protegido por el sistema operativo y no es accesible para la mayoría de los usuarios. Solo el sistema operativo y los administradores de sistema tienen acceso directo al SAM.

Cuando un usuario intenta iniciar sesión en un sistema Windows, el sistema verifica las credenciales proporcionadas por el usuario con la información almacenada en el archivo SAM. Si las credenciales coinciden, el usuario obtiene acceso al sistema. Este proceso de autenticación es crucial para garantizar la seguridad del sistema y proteger los datos de los usuarios.

# NTLM
NTLM, o "NT LAN Manager", es un protocolo de autenticación utilizado en sistemas operativos Windows para verificar la identidad de los usuarios y permitirles acceder a recursos compartidos en una red. NTLM puede trabajar en varios modos, pero uno de los más comunes es a través de hashes de contraseñas.

Cuando un usuario establece una contraseña en un sistema Windows, esta contraseña se convierte en un hash mediante un algoritmo de hash (como MD4 o MD5) y se almacena en el registro del sistema operativo, específicamente en el archivo SAM (Security Account Manager) mencionado anteriormente. Este hash es una representación cifrada de la contraseña y se utiliza durante el proceso de autenticación.

Cuando un usuario intenta iniciar sesión en un sistema Windows, el sistema solicita la contraseña del usuario. Luego, la contraseña ingresada por el usuario se convierte en un hash utilizando el mismo algoritmo de hash que se utilizó para almacenar la contraseña original. Este hash se compara con el hash almacenado en el archivo SAM. Si los hashes coinciden, el sistema permite el acceso al usuario.