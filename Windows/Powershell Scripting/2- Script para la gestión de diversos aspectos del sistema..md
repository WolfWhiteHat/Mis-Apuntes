```PowerShell
# Cabecera
<#
.SYNOPSIS
Script para la gestión de diversos aspectos del sistema.

.DESCRIPTION
Este script proporciona funciones para la monitorización del sistema, gestión de procesos y sistema de archivos.
Incluye funciones para obtener información sobre el estado del sistema, el sistema de archivos y los procesos en ejecución.

.AUTHOR
[Nombre del Grupo]
[Nombre de los Miembros]

.VERSION
1.0

.EXAMPLE
.\GestionSistema.ps1
#>

# Verificar si el usuario actual es administrador
$admin = ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")
if (-not $admin) {
    Write-Host "Este script requiere privilegios de administrador."
    exit
}

# Función para mostrar la ayuda/información de uso del script
function Mostrar-Ayuda {
    Write-Host "Uso del script GestionSistema.ps1"
    Write-Host "--------------------------"
    Write-Host "Este script proporciona funciones para la monitorización del sistema, gestión de procesos y sistema de archivos."
    Write-Host "No se requieren parámetros."
}

# Función para obtener el porcentaje de CPU utilizada y libre
function Obtener-PorcentajeCPU {
    $cpu = Get-Counter '\Processor(_Total)\% Processor Time'
    $cpuUsage = [math]::Round($cpu.CounterSamples.CookedValue, 2)
    $cpuFree = 100 - $cpuUsage
    Write-Host "Porcentaje de CPU utilizado: $cpuUsage%"
    Write-Host "Porcentaje de CPU libre: $cpuFree%"
}

# Función para obtener la cantidad de procesos activos en el sistema
function Obtener-CantidadProcesos {
    $procesos = Get-Process
    $cantidadProcesos = $procesos.Count
    Write-Host "Cantidad de procesos activos: $cantidadProcesos"
}

# Función para obtener el espacio total y libre del sistema de archivos
function Obtener-EspacioSistemaArchivos {
    $fs = Get-WmiObject Win32_LogicalDisk | Where-Object { $_.DriveType -eq 3 }
    foreach ($f in $fs) {
        $totalSpace = [math]::Round($f.Size / 1GB, 2)
        $freeSpace = [math]::Round($f.FreeSpace / 1GB, 2)
        Write-Host "Espacio total en $($f.DeviceID): $totalSpace GB"
        Write-Host "Espacio libre en $($f.DeviceID): $freeSpace GB"
    }
}

# Función para comprobar el estado del sistema y registrar eventos
function Comprobar-EstadoSistema {
    $cpu = Get-Counter '\Processor(_Total)\% Processor Time'
    $cpuUsage = [math]::Round($cpu.CounterSamples.CookedValue, 2)
    $mem = Get-WmiObject Win32_OperatingSystem
    $memUsage = [math]::Round(($mem.TotalVisibleMemorySize - $mem.FreePhysicalMemory) / $mem.TotalVisibleMemorySize * 100, 2)
    $fs = Get-WmiObject Win32_LogicalDisk | Where-Object { $_.DriveType -eq 3 }
    foreach ($f in $fs) {
        $fsFree = [math]::Round($f.FreeSpace / $f.Size * 100, 2)
        if ($memUsage -gt 80) {
            Write-Host "¡Alerta! La cantidad de memoria usada supera el 80%."
            Add-Content -Path "alerta.log" -Value "Alerta: La cantidad de memoria usada supera el 80%."
        }
        if ($cpuUsage -gt 85) {
            Write-Host "¡Alerta! El porcentaje de uso de la CPU supera el 85%."
            Add-Content -Path "alerta.log" -Value "Alerta: El porcentaje de uso de la CPU supera el 85%."
        }
        if ($fsFree -lt 15) {
            Write-Host "¡Alerta! El espacio libre en $($f.DeviceID) es inferior al 15%."
            Add-Content -Path "alerta.log" -Value "Alerta: El espacio libre en $($f.DeviceID) es inferior al 15%."
        }
    }
}

# Ejecución del script
Mostrar-Ayuda
Obtener-PorcentajeCPU
Obtener-CantidadProcesos
Obtener-EspacioSistemaArchivos
Comprobar-EstadoSistema

```

Explicación de cada parte del código:

1. **Cabecera**: Proporciona información detallada sobre el script, incluyendo su propósito, autor, versión y ejemplos de uso.
2. **Verificación de privilegios de administrador**: Se verifica si el usuario actual tiene privilegios de administrador. Si no los tiene, se muestra un mensaje de advertencia y se termina la ejecución del script.
3. **Función Mostrar-Ayuda**: Muestra información sobre cómo utilizar el script.
4. **Funciones para obtener información del sistema**:
    - `Obtener-PorcentajeCPU`: Obtiene el porcentaje de CPU utilizado y libre.
    - `Obtener-CantidadProcesos`: Obtiene la cantidad de procesos activos en el sistema.
    - `Obtener-EspacioSistemaArchivos`: Obtiene el espacio total y libre del sistema de archivos.
5. **Función para comprobar el estado del sistema**: Comprueba el estado del sistema, incluyendo la cantidad de memoria usada, el porcentaje de uso de la CPU y el espacio libre en el sistema de archivos. Registra eventos en un archivo de registro (`alerta.log`) si se superan ciertos umbrales.
6. **Ejecución del script**: Muestra la ayuda y luego ejecuta las funciones para obtener información del sistema y comprobar su estado.