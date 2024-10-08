Esta herramienta sirve para hacer escaneos web automáticos:
```bash
nikto -h http://192.8.241.3
```
![[Mis apuntes/ANEXOS/Pasted image 20230728115055.png]]

También podemos pasarle la URL de un target donde pensemos que pueda ser vulnerable a LFI:
![[Mis apuntes/ANEXOS/Pasted image 20230728115326.png]]

Por tanto hacemos la prueba:
```bash
nikto -h http://192.8.241.3/index.php?page=arbitrary-file-inclusion.php -Tuning 5 -Display V
```

Y nos lo encuentra:
![[Mis apuntes/ANEXOS/Pasted image 20230728115554.png]]

También podemos guardar este reporte en formato html:
```bash
nikto -h http://192.8.241.3/index.php?page=arbitrary-file-inclusion.php -Tuning 5 -Display V -o nikto.html -Format html
```
![[Mis apuntes/ANEXOS/Pasted image 20230728115759.png]]

Este comando lo utilizamos para hacer un escaneo web indicando que la web esta protegida por https
```Python
nikto -h https://nikto.org -ssl
```
