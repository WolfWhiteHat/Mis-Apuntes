Los Registros de Windows, conocidos como Windows Registry, son una base de datos jerárquica que almacena configuraciones y opciones de bajo nivel para el sistema operativo Microsoft Windows. Este registro contiene información y configuraciones para hardware, software, perfiles de usuario, y preferencias del sistema, entre otros. Actúa como un repositorio central para configurar las funciones y el comportamiento de casi todo en Windows, lo que lo hace un foco crucial tanto para la administración del sistema como para la seguridad informática.

# Tipos de registros
- `HKEY_CLASSES_ROOT`: Contiene información sobre las asociaciones de tipos de archivos y las propiedades de los objetos COM. Esencialmente, este registro ayuda a determinar qué programa se abrirá cuando interactúas con un archivo específico mediante una extensión o un enlace.
- `HKEY_CURRENT_USER`: Almacena configuraciones específicas del usuario actualmente conectado. Incluye preferencias de entorno de escritorio, configuraciones de software personalizadas y enlaces a archivos de datos.
- `HKEY_LOCAL_MACHINE`: Contiene una amplia gama de datos sobre la configuración del sistema, como configuraciones de hardware y software que son comunes a todos los usuarios en el equipo.
- `HKEY_USERS`: Incluye perfiles para todos los usuarios del sistema, cada uno representado por una subclave dentro de este registro. Contiene preferencias y configuración de usuario.
- `HKEY_CURRENT_CONFIG`: Contiene información sobre la configuración de hardware del sistema que se utiliza en el momento actual, como la configuración de gráficos y periféricos conectados.

# Tipos de datos
- `REG_SZ`: Este tipo almacena una cadena de texto sin formato. Es uno de los tipos más comunes y se utiliza para valores de configuración que consisten en texto legible, como rutas de acceso, nombres de equipos y otros parámetros de configuración.
- `REG_BINARY`: Almacena datos en formato binario. Es útil para datos que no necesitan ser legibles por humanos, como una contraseña cifrada o configuraciones específicas del sistema operativo.
- `REG_DWORD`: Almacena un número de 32 bits. Se utiliza para habilitar o deshabilitar características y funcionalidades, donde "0" podría representar deshabilitado y "1" habilitado, o para almacenar valores numéricos que no requieren más de 32 bits.
- `REG_QWORD`: Similar a `REG_DWORD`, pero almacena un número de 64 bits. Es útil para aplicaciones que necesitan almacenar grandes valores numéricos, como configuraciones de tiempo o capacidad.
- `REG_MULTI_SZ`: Utilizado para almacenar múltiples cadenas de texto, separadas por un carácter nulo y terminando también con un carácter nulo. Es ideal para listas de valores, como múltiples rutas de acceso o configuraciones que pueden tener varios valores.
- `REG_EXPAND_SZ`: Almacena cadenas de texto que contienen variables de entorno que se expanden automáticamente cuando el sistema o una aplicación accede a ellas. Esto es útil para referencias a rutas que pueden variar entre diferentes computadoras.
- `REG_NONE`: Indica que el tipo de datos no está definido. Esto se usa en circunstancias especiales donde los datos pueden no ajustarse a otros tipos predefinidos.
- `REG_LINK`: Almacena un enlace simbólico a otro valor en el registro. No es comúnmente utilizado por aplicaciones de terceros, pero es usado internamente por el sistema operativo.

# Comandos Reg
- **`reg add`**: Agrega una nueva subclave o entrada al registro.
- **`reg delete`**: Elimina una subclave o entrada del registro.
- **`reg copy`**: Copia una subclave de registro a otra ubicación.
- **`reg export`**: Exporta una subclave de registro a un archivo, útil para hacer copias de seguridad.
- **`reg import`**: Importa contenido de un archivo de registro al registro.
- **`reg load`**: Carga una subclave desde un archivo de disco al registro.
- **`reg unload`**: Descarga una subclave cargada previamente.
- **`reg query`**: Consulta el contenido de una subclave o entrada del registro.
- **`reg save`**: Guarda una subclave de registro en un archivo de disco.
- **`reg compare`**: Compara las diferencias entre dos subclaves de registro.
- **`reg restore`**: Restaura una subclave de registro desde un archivo de copia de seguridad.

## **Reg Query**
- **RootKey/SubKey**: Especifica la ruta completa de la clave de registro que quieres consultar.
- **/v ValueName**: Consulta por un nombre de valor específico bajo la clave especificada.
- **/ve**: Muestra el valor de la entrada predeterminada (sin nombre) para la clave especificada.
- **/s**: Consulta todas las subclaves y valores recursivamente.
- **/se**: Consulta todas las subclaves y valores recursivamente y muestra solo las entradas predeterminadas (sin nombre).
- **/f Data**: Busca en todas las subclaves, valores y datos, los registros que coincidan con los datos especificados.
- **/k**: Busca en las claves.
- **/d**: Busca en los datos.
- **/t Type**: Especifica el tipo de datos a buscar (por ejemplo, REG_SZ).
- **/c**: No diferencia mayúsculas de minúsculas en la búsqueda.
- **/e**: Devuelve solo las entradas que coinciden exactamente con los datos de búsqueda.