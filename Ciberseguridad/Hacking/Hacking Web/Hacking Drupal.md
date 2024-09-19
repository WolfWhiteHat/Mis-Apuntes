Para practicar vamos a utilizar este repositorio de github:
![[Mis apuntes/ANEXOS/Pasted image 20230422135923.png]]
Y lanzamos el docker: donde veremos que este drupal estará corriendo por el puerto 8080:
![[Mis apuntes/ANEXOS/Pasted image 20230422140036.png]]
![[Mis apuntes/ANEXOS/Pasted image 20230422140107.png]]
Y ya estamos ante la fase de instalación nuevamente:
![[Mis apuntes/ANEXOS/Pasted image 20230422140139.png]]
En este proceso de instalación tenemos que elegir el perfil de instalación estandar:
![[Mis apuntes/ANEXOS/Pasted image 20230422140226.png]]
Luego elegimos sqlite:
![[Mis apuntes/ANEXOS/Pasted image 20230422140253.png]]
Y completamos la configuración con la contraseña password1:
![[Mis apuntes/ANEXOS/Pasted image 20230422140425.png]]
Y así debería quedarnos todo:
![[Mis apuntes/ANEXOS/Pasted image 20230422140505.png]]
## EXPLOTACIÓN DE DRUPAL
Ahora vamos a empezar la fase de reconocimiento y explotación de un drupal, donde en primer lugar con whatweb veremos ante qué nos estamos enfrendando:
![[Mis apuntes/ANEXOS/Pasted image 20230422140640.png]]
Si queremos utilizar una herramienta para escanear las vulnerabilidades de un drupal, podemos usar droopescan:
![[Mis apuntes/ANEXOS/Pasted image 20230422140752.png]]
Nos clonamos este repositorio y procedemos con la instalación. En primer lugar con las dependencias:
![[Mis apuntes/ANEXOS/Pasted image 20230422140918.png]]Y ahora ejecutamos el instalador que también está dentro de la carpeta de este repositorio:
![[Mis apuntes/ANEXOS/Pasted image 20230422141018.png]]
Y ya lo tenemos correctamente instalado:
![[Mis apuntes/ANEXOS/Pasted image 20230422141042.png]]
Y si ejecutamos esta herramienta con estos parámetros ya podremos ver características de este drupal, aunque en este caso no encuentra gran cosa, pero en otras ocasiones sí puede encontrar algo:
![[Mis apuntes/ANEXOS/Pasted image 20230422141402.png]]
Y ahora que conocemos la versión, podríamos buscar vulnerabilidades con searchsploit [[MAQUINA ARMAGEDDON (Vulnerabilidad Drupal 7 con metasploit, escalada privilegios obteniendo credenciales de mysql y entrando y vulnerabilidad snap con dirty shock)]]:
![[Mis apuntes/ANEXOS/Pasted image 20230422141514.png]]
