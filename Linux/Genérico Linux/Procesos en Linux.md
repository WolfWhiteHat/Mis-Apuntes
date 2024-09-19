**Mandar un proceso al segundo plano**
Podemos ejecutar un comando y dejarlo en segundo plano si le añadimos un &:
```bash
firefox &
```
![[Pasted image 20231225111959.png]]
Y con el comando ps aux podemos ver cómo encontramos el proceso de firefox corriendo:
![[Pasted image 20231225112058.png]]
**Detener un Proceso**
Para detener un proceso, primero ejecutamos el comando pgrep para conocer el PID del proceso, y luego con kill lo detenemos:
![[Pasted image 20231225112445.png]]
**Comando JOBS**
Con este comando podemos ver cómo firefox se encuentra corriendo:
![[Pasted image 20231225112213.png]]
Podemos pasar este proceso al primer plano con el comando fg:
![[Pasted image 20231225112654.png]]
Para suspender un trabajo, podemos pulsar ctrl+Z:
![[Pasted image 20231225112820.png]]
Y este mismo proceso podemos mandarlo al segundo plano con el comando bg:
```bash
bg
```
![[Pasted image 20231225112926.png]]
**Traer un proceso del segundo plano al primer plano**
Primero ejecutamos el comando jobs para conocer el número del trabajo, y luego lo traemos con fg:
```bash
fg %1
```
![[Pasted image 20231225113117.png]]