Es una herramienta de código abierto utilizada en pruebas de penetración y auditorías de seguridad para enumerar información de sistemas Windows y servicios SMB (Server Message Block) dentro de una red. Permite a los investigadores obtener información valiosa sobre usuarios, grupos, recursos compartidos y políticas de seguridad en sistemas Windows utilizando el protocolo SMB.

# Comandos Enum4linux
![[Pasted image 20240304164956.png]]

# Enumeración sencilla
```Bash
enum4linux -a
```
![[Pasted image 20240604073319.png]]

## Información SO
enum4linux -o [IP]
![[Pasted image 20240304165823.png]]

# Listar usuarios
```Bash
enum4linux -U [IP]
```
![[Pasted image 20240304165851.png]]

enum4linux -S [IP]
![[Pasted image 20240304172701.png]]
![[Pasted image 20240304172725.png]]

## Obtener SID
enum4linux -r -u "admin" -p "password1" [IP]
![[Pasted image 20240304185253.png]]
![[Pasted image 20240304185310.png]]