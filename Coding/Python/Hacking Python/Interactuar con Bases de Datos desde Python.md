Lo primero será instalar esta librería de Python para gestionar bases de datos MySQL desde Python:
![[Mis apuntes/ANEXOS/Pasted image 20221217093730.png]]
Y lo primero será establecer la conexión:
![[Mis apuntes/ANEXOS/Pasted image 20221217093748.png]]
![[Mis apuntes/ANEXOS/Pasted image 20221217093755.png]]
Ahora vamos a hacer una consulta:
```python
import mysql.connector

connection = mysql.connector.connect(user='root', password='123123',
                                    host='localhost',
                                    database='hr',
                                    port='3306',)

print(connection)

cursor = connection.cursor()
cursor.execute("SELECT first_name FROM employees")

consulta = cursor.fetchall()
print(consulta)
```
![[Mis apuntes/ANEXOS/Pasted image 20221217093818.png]]
Ahora vamos a procesar esta consulta para volcarla dentro de un documento de texto:
![[Mis apuntes/ANEXOS/Pasted image 20221217093834.png]]
![[Mis apuntes/ANEXOS/Pasted image 20221217093839.png]]
