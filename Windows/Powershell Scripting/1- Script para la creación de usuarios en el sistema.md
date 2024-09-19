``` PowerShell
# Cabecera
<#
.SYNOPSIS
Script para la creación de usuarios en el sistema.

.DESCRIPTION
Este script permite al administrador crear usuarios en el sistema de forma automatizada. 
Incluye funciones para verificar la existencia de usuarios y grupos, así como para crear nuevos usuarios y grupos.

.AUTHOR
[Nombre del Grupo]
[Nombre de los Miembros]

.VERSION
1.0

.PARAMETER UserName
Nombre de usuario a crear.

.PARAMETER FullName
Nombre completo del usuario.

.PARAMETER Password
Contraseña del usuario.

.PARAMETER GroupName
Nombre del grupo al que pertenecerá el usuario.

.EXAMPLE
.\CrearUsuario.ps1 -UserName "UsuarioNuevo" -FullName "Nombre Completo" -Password "Password123" -GroupName "GrupoEjemplo"
#>

# Verificar si el usuario actual es administrador
$admin = ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")
if (-not $admin) {
    Write-Host "Este script requiere privilegios de administrador."
    exit
}

# Función para mostrar la ayuda/información de uso del script
function Mostrar-Ayuda {
    Write-Host "Uso del script CrearUsuario.ps1"
    Write-Host "--------------------------"
    Write-Host "Este script permite la creación de usuarios en el sistema."
    Write-Host "Parámetros:"
    Write-Host "-UserName    : Nombre de usuario a crear."
    Write-Host "-FullName    : Nombre completo del usuario."
    Write-Host "-Password    : Contraseña del usuario."
    Write-Host "-GroupName   : Nombre del grupo al que pertenecerá el usuario."
}

# Función para verificar si un usuario existe
function Verificar-UsuarioExistente {
    param(
        [string]$UserName
    )
    $user = Get-LocalUser -Name $UserName -ErrorAction SilentlyContinue
    if ($user -ne $null) {
        return $true
    } else {
        return $false
    }
}

# Función para verificar si un grupo existe
function Verificar-GrupoExistente {
    param(
        [string]$GroupName
    )
    $group = Get-LocalGroup -Name $GroupName -ErrorAction SilentlyContinue
    if ($group -ne $null) {
        return $true
    } else {
        return $false
    }
}

# Función para crear un nuevo usuario
function Crear-NuevoUsuario {
    param(
        [string]$UserName,
        [string]$FullName,
        [string]$Password,
        [string]$GroupName
    )
    if (Verificar-UsuarioExistente -UserName $UserName) {
        Write-Host "El usuario '$UserName' ya existe en el sistema."
        return
    }
    if (-not (Verificar-GrupoExistente -GroupName $GroupName)) {
        Write-Host "El grupo '$GroupName' no existe en el sistema."
        return
    }
    $SecurePassword = ConvertTo-SecureString -String $Password -AsPlainText -Force
    New-LocalUser -Name $UserName -FullName $FullName -Password $SecurePassword -Group $GroupName
    Write-Host "Usuario '$UserName' creado correctamente."
}

# Función para crear un nuevo grupo
function Crear-NuevoGrupo {
    param(
        [string]$GroupName
    )
    if (Verificar-GrupoExistente -GroupName $GroupName) {
        Write-Host "El grupo '$GroupName' ya existe en el sistema."
        return
    }
    New-LocalGroup -Name $GroupName
    Write-Host "Grupo '$GroupName' creado correctamente."
}

# Ejecución del script
param (
    [string]$UserName,
    [string]$FullName,
    [string]$Password,
    [string]$GroupName
)

# Mostrar ayuda si no se proporcionan parámetros
if (-not $UserName -or -not $FullName -or -not $Password -or -not $GroupName) {
    Mostrar-Ayuda
    exit
}

# Crear nuevo usuario y grupo
Crear-NuevoUsuario -UserName $UserName -FullName $FullName -Password $Password -GroupName $GroupName

```

Explicación de cada parte del código:

1. **Cabecera**: Proporciona información detallada sobre el script, incluyendo su propósito, autor, versión, parámetros de entrada y ejemplos de uso.
2. **Verificación de privilegios de administrador**: Utiliza la clase `[Security.Principal.WindowsPrincipal]` para verificar si el usuario actual tiene privilegios de administrador. Si no los tiene, muestra un mensaje de advertencia y termina la ejecución del script.
3. **Función Mostrar-Ayuda**: Esta función muestra información sobre cómo utilizar el script, incluyendo una descripción del propósito del script y los parámetros requeridos.
4. **Funciones de verificación**: `Verificar-UsuarioExistente` y `Verificar-GrupoExistente` comprueban si un usuario o grupo ya existen en el sistema.
5. **Funciones de creación**: `Crear-NuevoUsuario` y `Crear-NuevoGrupo` crean un nuevo usuario y grupo, respectivamente, si no existen previamente.
6. **Ejecución del script**: Verifica si se proporcionan todos los parámetros requeridos y, si es así, llama a la función `Crear-NuevoUsuario` para crear un nuevo usuario y agregarlo al grupo especificado.