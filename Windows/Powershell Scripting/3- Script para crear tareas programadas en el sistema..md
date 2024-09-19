```PowerShell
# Cabecera
<#
.SYNOPSIS
Script para crear tareas programadas en el sistema.

.DESCRIPTION
Este script permite al administrador del sistema automatizar tareas mediante la programación de tareas en el sistema.
Puede llamar a los scripts anteriores pasándoles parámetros de entrada para realizar diversas tareas.

.AUTHOR
[Nombre del Grupo]
[Nombre de los Miembros]

.VERSION
1.0

.EXAMPLE
.\CrearTareasProgramadas.ps1
#>

# Verificar si el usuario actual es administrador
$admin = ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")
if (-not $admin) {
    Write-Host "Este script requiere privilegios de administrador."
    exit
}

# Función para mostrar la ayuda/información de uso del script
function Mostrar-Ayuda {
    Write-Host "Uso del script CrearTareasProgramadas.ps1"
    Write-Host "--------------------------"
    Write-Host "Este script permite al administrador del sistema automatizar tareas mediante la programación de tareas en el sistema."
    Write-Host "No se requieren parámetros."
}

# Función para crear una tarea programada
function Crear-TareaProgramada {
    param(
        [string]$TipoTarea
    )
    switch ($TipoTarea) {
        "Monitorizacion" {
            # Llamar al script de monitorización del sistema
            .\GestionSistema.ps1
        }
        "BuscarFicheros" {
            # Solicitar parámetros al usuario
            $Usuarios = Read-Host "Ingrese nombres de usuario separados por comas"
            $Extension = Read-Host "Ingrese la extensión de archivo a buscar"
            # Llamar al script de búsqueda de archivos con los parámetros proporcionados
            .\BuscarArchivos.ps1 -Usuarios $Usuarios -Extension $Extension
        }
        default {
            Write-Host "Tipo de tarea no válido."
        }
    }
}

# Ejecución del script
Mostrar-Ayuda
$TipoTarea = Read-Host "Seleccione el tipo de tarea a automatizar (Monitorizacion/BuscarFicheros)"
Crear-TareaProgramada -TipoTarea $TipoTarea

```

Explicación de cada parte del código:

1. **Cabecera**: Proporciona información detallada sobre el script, incluyendo su propósito, autor, versión y ejemplos de uso.
2. **Verificación de privilegios de administrador**: Se verifica si el usuario actual tiene privilegios de administrador. Si no los tiene, se muestra un mensaje de advertencia y se termina la ejecución del script.
3. **Función Mostrar-Ayuda**: Muestra información sobre cómo utilizar el script.
4. **Función para crear una tarea programada**: Esta función permite al usuario seleccionar el tipo de tarea que desea automatizar. Dependiendo del tipo de tarea seleccionada, se llamará al script correspondiente con los parámetros necesarios.
5. **Ejecución del script**: Muestra la ayuda y luego solicita al usuario que seleccione el tipo de tarea a automatizar. Luego, llama a la función `Crear-TareaProgramada` con el tipo de tarea seleccionado como parámetro.