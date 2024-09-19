TTL significa "Time to Live" (Tiempo de Vida) y es un campo en los encabezados de los paquetes IP que indica cuántos saltos (routers) puede atravesar un paquete antes de que sea descartado. El TTL se utiliza principalmente para evitar que los paquetes queden atrapados en bucles de enrutamiento infinitos. Cada vez que un router recibe un paquete, decrementa el valor del TTL en una unidad. Si el TTL llega a cero, el router descarta el paquete y envía un mensaje de error de "Tiempo Excedido" (Time Exceeded) de vuelta al remitente.

### Detección TTL

- `Linux`: 64
- `FreBSD`64
- `Windows`: 128
- `Mac`:64
- `IOS`: 255
- `Cisco`: 255
![[Pasted image 20240112103316.png]]