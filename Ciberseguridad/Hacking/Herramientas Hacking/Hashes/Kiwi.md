En Metasploit, "Kiwi" es un módulo que se refiere a las herramientas y técnicas utilizadas para realizar ataques de explotación y post-explotación en sistemas Windows. Específicamente, Kiwi se centra en la explotación de credenciales y la extracción de información sensible de sistemas comprometidos.

El término "Kiwi" se originó en el proyecto Mimikatz, una herramienta popular utilizada para la extracción de credenciales de sistemas Windows. Metasploit incorporó funcionalidades similares a las ofrecidas por Mimikatz bajo el nombre de "Kiwi", lo que permite a los usuarios llevar a cabo acciones como el robo de contraseñas almacenadas en memoria, la extracción de tickets Kerberos, la recuperación de credenciales de aplicaciones, entre otras.

El funcionamiento de Kiwi en Metasploit implica la carga de un módulo específico que incluye las capacidades de extracción de credenciales deseadas. Una vez que se ha comprometido un sistema objetivo, los usuarios pueden utilizar los módulos de Kiwi para extraer credenciales almacenadas en la memoria del sistema comprometido. Estas credenciales pueden incluir contraseñas de usuario, hashes NTLM, tickets Kerberos, claves de cifrado, entre otros datos sensibles.

La ejecución de un módulo de Kiwi en Metasploit generalmente sigue estos pasos:

1. Identificación del sistema objetivo y selección de un exploit adecuado para obtener acceso.
2. Explotación del sistema objetivo para obtener acceso a través de una shell o sesión de Metasploit.
3. Carga del módulo Kiwi relevante que se adapte a los objetivos específicos de extracción de credenciales.
4. Ejecución del módulo Kiwi para extraer las credenciales del sistema comprometido.
5. Posteriormente, las credenciales extraídas pueden ser utilizadas para realizar movimientos laterales en la red comprometida, escalar privilegios u obtener acceso a recursos adicionales.

Es importante destacar que el uso de Kiwi en Metasploit debe realizarse con fines éticos y legales, y con el consentimiento adecuado del propietario del sistema o la red objetivo. El uso no autorizado de estas técnicas puede tener consecuencias legales graves.


### Comandos
- `creds`: Este comando muestra las credenciales recuperadas del sistema comprometido, como contraseñas en texto plano, hashes de contraseñas, tickets Kerberos, etc.
- `creds_all`: Similar al comando anterior, pero este muestra todas las credenciales disponibles, incluso las que podrían no ser útiles para la sesión actual.
- `extract`: Este comando permite extraer información específica de las credenciales, como hashes de contraseñas o tickets Kerberos, y almacenarla en archivos separados para un uso posterior.
- `kerberos`: Este comando muestra los tickets Kerberos (TGT y TGS) presentes en el sistema comprometido y los descifra si es posible, revelando información sobre los usuarios autenticados y los servicios a los que tienen acceso.
- `mimikatz_command`: Este comando permite ejecutar comandos personalizados de Mimikatz en el sistema comprometido, lo que proporciona flexibilidad para realizar acciones específicas no cubiertas por otros comandos de Kiwi.
- `dump`: Este comando realiza un volcado de la memoria del sistema comprometido y busca credenciales en los datos extraídos, como contraseñas en texto plano o hashes.
- `hashdump`: Similar al comando anterior, pero se centra específicamente en extraer hashes de contraseñas del sistema comprometido.
- `search`: Este comando permite buscar en la memoria del sistema comprometido para encontrar credenciales específicas, como nombres de usuario, contraseñas u otros datos sensibles.
- `hash`: Muestra los hashes de contraseñas almacenados en el sistema comprometido, lo que puede ser útil para realizar ataques de fuerza bruta o de diccionario.
- `kiwi::logonpasswords`: Este comando muestra las contraseñas en texto plano de las sesiones de inicio de sesión activas en el sistema comprometido, lo que puede revelar información valiosa sobre las credenciales utilizadas por los usuarios.
- `mimikatz`: Este comando permite ejecutar varias funciones de Mimikatz en el sistema comprometido, incluida la extracción de credenciales, la manipulación de tokens, la visualización de tickets Kerberos, entre otros.
- `net`: Muestra las credenciales almacenadas en caché por aplicaciones y servicios de red en el sistema comprometido, lo que puede revelar información sobre la autenticación pasada y actual.
- `ekeys`: Muestra las claves de cifrado almacenadas en el sistema comprometido, lo que puede ser útil para descifrar datos encriptados o realizar ataques criptográficos.
- `pfx`: Muestra los certificados y claves privadas almacenadas en el sistema comprometido, lo que puede proporcionar acceso a recursos protegidos por autenticación SSL/TLS.

# Ejemplo

## Hash NT
creds_all
![[Pasted image 20240312073512.png]]

Ahora con el siguiente comando sacaremos el valor hash de todos los usuarios
lsa_dump_sam
![[Pasted image 20240312073612.png]]

## Hash LM
hashdump
![[Pasted image 20240312082110.png]]