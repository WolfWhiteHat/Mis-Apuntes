Es un administrador de tareas en segundo plano que se ejecuta en sistemas operativos tipo Unix, que permite a los usuarios programar tareas para que se ejecuten automáticamente en un momento o intervalo específico.

El cron utiliza archivos llamados "crontabs" para definir las tareas a ejecutar y su programación. Cada usuario puede tener su propio crontab, y también hay un crontab de sistema que se utiliza para tareas del sistema.

El formato de un crontab es el siguiente:
[minutos] [horas] [día del mes] [mes] [día de la semana] comando_a_ejecutar

Ejemplo de un crontab que se ejecuta todos los días a las 3 AM:
0 3 * * * /ruta/al/comando
