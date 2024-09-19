`schtasks` se utiliza para crear, eliminar, configurar o mostrar tareas programadas en Windows. Es especialmente útil para establecer persistencia o para ejecutar cargas útiles en un horario específico.

# Listar todas las tareas programadas
```
schtasks /query /fo LIST
```

# Modificar tarea existente para ejecutar carga util
```
schtasks /change /tn "ExistingTask" /tr "C:\path\to\newpayload.bat"
```
