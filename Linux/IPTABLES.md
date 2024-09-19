# Comandos
- INPUT: Trafico entrante
- OUTPUT: Trafico saliente
- FORWARD: Reenvio de trafico, se aplican las reglas a todos los paquetes que pasan por el sistema pero que el destinatario es otro sistema

Las reglas pueden ser TCP o UDP
# Politicas predeterminadas
## **Prohibir trafico entrante**
```
iptables -P INPUT DROP
```
![[Pasted image 20240215100609.png]]
## **Prohibir trafico saliente**
```
iptables -P OUTPUT DROP
```
![[Pasted image 20240215100822.png]]

## **Prohibir filtrado de paquetes por reglas**
```
iptables -P FORWARD DROP
```
![[Pasted image 20240215100902.png]]

## **Permitir trafico entrante**
```
iptables -P INPUT ACCEPT
```
![[Pasted image 20240215101134.png]]

## **Permitir trafico saliente**
```
iptables -P OUTPUT ACCEPT
```
![[Pasted image 20240215101201.png]]

## **Permitir filtrado de paquetes por reglas**
```
iptables -P FORWARD ACCEPT
```
![[Pasted image 20240215101417.png]]

## **Permitir trafico puerto 80**
```
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```
![[Pasted image 20240215095448.png]]

## **Denegar trafico puerto 80**
```
iptables -A INPUT -p tcp --dport 80 -j DROP
```
![[Pasted image 20240215101514.png]]

## **Mostrar todas las reglas**
```
iptables -L -v
```
![[Pasted image 20240215095557.png]]

## **Eliminar reglas**
```
iptables -D INPUT 1
```
![[Pasted image 20240215095908.png]]

# Reglas Forward
## **Permitir reenvio de paquetes de una interfaz a otra**
```
iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT
```
![[Pasted image 20240215102551.png]]

## **Bloquear todo el trafico de reenvio entre dos subredes**
```
iptables -A FORWARD -s 192.168.1.0/24 -d 10.0.0.0/24 -j DROP
```
![[Pasted image 20240215102629.png]]

## **Guardar reglas**
```
iptables-save > /home/wolf/Escriotrio/iptables
```
![[Pasted image 20240215100112.png]]

## **Restaurar reglas**
```
iptables-restore < /home/wolf/Escriotrio/iptables
```
![[Pasted image 20240215100422.png]]

## **Eliminar todas las reglas**
```
iptables -F
```
![[Pasted image 20240215100726.png]]

## **Revisar puertos abiertos**
```
netstat -tuln
```
![[Pasted image 20240304082110.png]]

```
ss -tuln 
```
![[Pasted image 20240304082246.png|1000]]

```
nmap localhost
```
![[Pasted image 20240304082514.png]]
