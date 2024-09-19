Shodan es un motor de búsqueda que permite encontrar dispositivos conectados a Internet. Funciona escaneando Internet en busca de dispositivos que estén escuchando en determinados puertos. Cuando encuentra un dispositivo, Shodan recopila información sobre él, como su dirección IP, el puerto en el que está escuchando y el software que está ejecutando.
Puede utilizarse para encontrar vulnerabilidades en los dispositivos conectados a Internet, para rastrear el origen de los ataques cibernéticos y para recopilar información sobre la infraestructura de Internet.

Aquí tienes algunos ejemplos de cómo se puede utilizar Shodan:

- Encontrar cámaras web que estén expuestas a Internet.
- Encontrar servidores que estén ejecutando software vulnerable.
- Rastrear el origen de los ataques cibernéticos.
- Recopilar información sobre la infraestructura de Internet.

Web oficial:
https://www.shodan.io
![[Pasted image 20240207085327.png|750]]
En el buscador de shodan podemos buscar por ip la información desedad, nosotros buscamos la ip de una web haciendo ping y podremos buscar posteriormente en el navegador.

Sacamos la ip en este caso de la de web de una empresa
![[Pasted image 20240207090040.png]]

Una vez tenemos la ip nos vamos a la web y la añadimos
![[Pasted image 20240207090117.png]]

![[Pasted image 20240207090149.png]]
![[Pasted image 20240207091825.png]]
Aquí ya nos esta dando información sobre la web, el proveedor, su ubicación, puertos abiertos, servicios que utiliza.

Vamos a seleccionar otra IP
![[Pasted image 20240207091952.png]]
![[Pasted image 20240207092031.png]]

Aquí nos esta dando un dominio, si accedemos obtendremos mas información
![[Pasted image 20240207092109.png]]
### ASN
El ASN (Autonomous System Number) es un identificador único de 16 bits asignado a cada red autónoma en Internet. Se utiliza para enrutar el tráfico entre diferentes redes y para identificar la red a la que pertenece un determinado dispositivo.

Los ASN son asignados por la Autoridad de Números Asignados de Internet (IANA) y se pueden utilizar para rastrear el origen del tráfico de Internet y para identificar las redes que están conectadas a Internet.

Cada red autónoma tiene un ASN único, y este ASN se utiliza para identificar la red en los protocolos de enrutamiento. Cuando un paquete de datos se envía a través de Internet, el ASN del remitente se incluye en el paquete. Esto permite a los routers enrutar el paquete a la red correcta.

Los ASN también se utilizan para identificar las redes que están conectadas a Internet. Cuando una red se conecta a Internet, se le asigna un ASN. Este ASN se utiliza para identificar la red en los registros de Internet y en los directorios de enrutamiento.

Como podemos ver en la siguiente imagen si clickamos en el ASN una vez buscada la ip nos mostrara la siguiente información, esto lo podemos hacer a mano escribiendolo directamente en el buscador de shodan
![[Pasted image 20240207092948.png]]
![[Pasted image 20240207092826.png]]

Shodan también se puede utilizar desde el termianl, para ellos seguiremos los sigueintes pasos.

Primero instalaremos Python3, en mi caso ya estaba instalado y solo faltaba verificarlo
![[Pasted image 20240207093306.png]]

Con el siguiente comando instalamos shodan
brew install shodan
![[Pasted image 20240207093603.png]]

Para verificar que esta instalado correctamente escribiremos shodan
![[Pasted image 20240207093700.png]]

Ahora que ya tenemos instalado shodan para poder utilizarlo deberemos ir a la web y añadir la API KEY, para ello nos vamos a la web y arriba a la derecha una vez estemos logueados nos aparecera un boton de Account
![[Pasted image 20240207093853.png]]

Al entrar nos mostrara información de nuestra cuenta y debajo nos saldra un boton para generar la api
![[Pasted image 20240207094007.png]]

Desde la terminal escribimos el siguiente comando
shodan init API_KEY
![[Pasted image 20240207094121.png]]

Como podemos ver ya nos esta informando que esta shodan preparado en nuestro dispositivo.

Para hacer la prueba si escribimos shodan -h podremos ver los comandos que a utilizar
![[Pasted image 20240207094241.png]]