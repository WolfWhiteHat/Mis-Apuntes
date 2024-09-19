Es una funcionalidad dentro del framework Metasploit que automatiza el proceso de búsqueda, exploración y explotación de vulnerabilidades en sistemas informáticos.

Metasploit-Autopwn permite a los usuarios escanear una red o un conjunto de sistemas en busca de vulnerabilidades conocidas, identificar posibles puntos de entrada, seleccionar y lanzar automáticamente exploits contra esos puntos débiles identificados. Esto puede simplificar y acelerar el proceso de búsqueda y explotación de vulnerabilidades

https://github.com/hahwul/metasploit-autopwn


Descargamos el repositorio en nuestro sistema
wget https://raw.githubusercontent.com/hahwul/metasploit-autopwn/master/db_autopwn.rb

Accedemos al directorio y movemos el pluging a la siguiente ruta
cd metasploit-autopwn
cp db_autopwn.rb /usr/share/metasploit-framework/plugins


Para utilizarlo utilizaremos el siguiente comando
db_autopwn -p -t 


Para realizar busquedas avanzadas de los exploits que tenemos en nuestra base de datos podemos usar el comando `analyze`