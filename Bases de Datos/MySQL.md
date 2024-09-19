
# Comandos BBDD
- `ALTER TABLE`: Modifica la estructura de una tabla existente.
- `ALTER USER`: Modifica los privilegios o la configuración de un usuario en la base de datos.
- `BACKUP`: Realiza una copia de seguridad de la base de datos.
- `BEGIN`: Inicia una transacción.
- `COMMIT`: Confirma los cambios realizados dentro de una transacción.
- `CREATE INDEX`: Crea un índice en una tabla para acelerar las consultas.
- `CREATE TABLE`: Crea una nueva tabla en la base de datos.
- `DELETE`: Elimina registros de una tabla.
- `DESCRIBE o DESC`: Muestra la estructura de una tabla.
- `DROP DATABASE`: Elimina una base de datos completa.
- `DROP INDEX`: Elimina un índice existente de una tabla.
- `DROP TABLE`: Elimina una tabla de la base de datos.
- `GRANT`: Concede privilegios a un usuario sobre una base de datos u objetos dentro de ella.
- `GRANT ALL PRIVILEGES`: Concede todos los privilegios disponibles sobre una base de datos u objetos dentro de ella a un usuario.
- `REVOKE`: Revoca privilegios previamente concedidos a un usuario.
- `REVOKE ALL PRIVILEGES`: Revoca todos los privilegios de un usuario sobre una base de datos u objetos dentro de ella.
- `ROLLBACK`: Deshace los cambios realizados dentro de una transacción.
- `SELECT`: Recupera datos de una base de datos.
- `SELECT DISTINCT`: Se utiliza para seleccionar valores únicos de una columna.
- `SHOW COLUMNS`: Muestra la estructura de columnas de una tabla específica.
- `SHOW CREATE TABLE`: Muestra el SQL utilizado para crear una tabla específica.
- `SHOW DATABASES`: Muestra una lista de las bases de datos disponibles en el servidor.
- `SHOW GRANTS`: Muestra los privilegios concedidos a un usuario específico.
- `SHOW INDEX`: Muestra los índices definidos en una tabla.
- `SHOW PROCESSLIST`: Muestra una lista de procesos que se están ejecutando en el servidor de la base de datos en ese momento.
- `SHOW TABLES`: Muestra una lista de las tablas en la base de datos actual.
- `TRUNCATE TABLE`: Elimina todos los registros de una tabla, pero conserva su estructura.
- `UPDATE`: Actualiza registros existentes en una tabla.
- `HELP`: Muestra ayuda con los comandos

Al terminar cada comando añadir `;`


## Conectar BBDD

### MySQL/MariaDB
mysql -u usuario -p -h [IP]
- `-u`: Especifica el nombre de usuario.
- `-p`: Solicita la contraseña del usuario.
- `-h`: Especifica el host donde se encuentra la base de datos.


### PostgreSQL
psql -U usuario -d basededatos -h [IP]
- `-U`: Especifica el nombre de usuario.
- `-d`: Especifica el nombre de la base de datos a la que deseas conectarte.
- `-h`: Especifica el host donde se encuentra la base de datos.


### SQLLite
sqlite3 ruta_a_la_base_de_datos
Donde `ruta_a_la_base_de_datos` es la ruta al archivo de la base de datos SQLite.


### Listar BBDD
show databases
![[Pasted image 20240521130901.png]]

# Listar tablas
```Bash
show full tables
```
![[Pasted image 20240521130954.png]]
### Seleccionar tabla
use [table]