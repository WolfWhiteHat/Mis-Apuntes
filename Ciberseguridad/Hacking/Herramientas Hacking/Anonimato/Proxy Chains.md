Configurar proxy chains

apt update -y
apt install proxychains

Ahora editaremos el fichero proxychains
nano /etc/proxychains.conf

#### Estructura
protocolo ip puerto

### Ejecutar proxyChains
sudo proxychains curl ifconfig.me; echo -e "\n"

### Detalles del proxy
sudo tail -n1 /etc/proxychains.conf

### Modos de ProxyChains
#### Strict Chain
Es el modo por defecto y su configuración es lineal, es decir sigue el orden de configuración por ejemplo de A a B y luego a la C, si uno de los proxys falla por el camino se cortara la comunicación

#### Dynamic Chain
Es similar a la configuración anterior con la diferencia de que en el caso de que un proxy caiga, este será saltado y pasara al siguiente dándonos mas seguridad en los paquetes

#### Random Chain
A diferencia de los otros en este caso no sigue ningún orden, selecciona los proxy de forma aleatoria y no sabes porque orden de proxys pasara.

### Protocolos a configurar
- HTTP
- HTTPS
- Socks4
- Socks5
- TCP
- UDP

### Encontrar los proxys
https://hidemy.io/en/proxy-list/

