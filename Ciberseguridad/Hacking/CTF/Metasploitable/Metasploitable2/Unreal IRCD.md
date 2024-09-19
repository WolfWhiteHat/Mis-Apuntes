Vamos a buscar explotarlas, para ellos iniciaremos metasploit con el siguiente comando
msfconsole
![[Pasted image 20240129124523.png]]

Una vez dentro buscaremos si metasploit tiene encuantra algun exploit para la  vulnerabilidad seleccionada, en este caso hemos buscado UnrealIRCD que es la vulnerabilidad que vamos a explotar
![[Pasted image 20240129124712.png]]

Una vez la encontramos y decidimos que es la que vamos a utilizar, la selecionamos y empezaremos a preparar el ataque, con el siguiente comando podremos ver la configuración que tenemos para realizar el ataque
![[Pasted image 20240129125313.png]]

Ahora necesitaremos seleccionar un payload, para ello escribimos show payload para revisarlos
![[Pasted image 20240129130656.png]]
Una vez vemos el payload que queremos selecciona con el comando set payload y su ID lo seleccionaremos, en este caso vamos a seleccionar el 5 que es para realizar un rever shell

Una vez tenemos seleccionado el payload ahora nos queda indicar la victima, para ello seleccionamos set RHOSTS [IP]
![[Pasted image 20240129131326.png]]


Ahora solo quedaria seleccionar nuetra ip local (localhost) porque tenemos que configurar que maquina sera la que escuche y haga el reverse shell
![[Pasted image 20240129131720.png]]
Aqui ya podemos ver que esta todo preparado para realizar el ataque, unicamente faltaria ejecutarlo, para ello escribimos run

![[Pasted image 20240129131912.png]]
Y ya estariamos conectados a la maquina de la victima
![[Pasted image 20240129131956.png]]
Aquí podemos ver que hemos realizado una consulta dentro de la maquina.