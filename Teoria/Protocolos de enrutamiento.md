# 1. RIP (Routing Information Protocol)
- **Tipo:** Protocolo de enrutamiento de vector de distancia.
- **Descripción:** Usa el número de saltos (hops) como métrica para determinar la mejor ruta hacia un destino. Su límite de saltos es de 15, lo que lo hace adecuado solo para redes pequeñas.
- **Versión actual:** RIP v2, que admite autenticación y el uso de direcciones de subred (CIDR).
- **Uso:** Generalmente en redes pequeñas y entornos de bajo costo donde la simplicidad es clave.

# 2. OSPF (Open Shortest Path First)
- **Tipo:** Protocolo de estado de enlace.
- **Descripción:** Usa el algoritmo SPF (Shortest Path First) para calcular la ruta más corta basada en el coste de cada enlace. Es escalable y se utiliza en grandes redes empresariales y de proveedores de servicios.
- **Características:** Soporta división en áreas y utiliza el concepto de zona backbone para optimizar el enrutamiento en grandes redes.
- **Uso:** Muy popular en redes empresariales grandes, debido a su escalabilidad y eficiencia.

# 3. EIGRP (Enhanced Interior Gateway Routing Protocol)
- **Tipo:** Protocolo híbrido (combinación de vector de distancia y estado de enlace).
- **Descripción:** Propietario de Cisco, es una mejora del protocolo IGRP. EIGRP es eficiente en el uso del ancho de banda y permite una rápida convergencia.
- **Características:** Calcula rutas basándose en métricas como ancho de banda, retraso, carga y confiabilidad.
- **Uso:** Común en redes que utilizan equipos Cisco, ya que es exclusivo de esta marca.

# 4. BGP (Border Gateway Protocol)
- **Tipo:** Protocolo de enrutamiento entre dominios autónomos (protocolo de pasarela exterior).
- **Descripción:** Es el protocolo que sostiene el funcionamiento de Internet. Usa una tabla de prefijos de rutas para intercambiar información entre sistemas autónomos (AS). El BGP toma decisiones basadas en políticas, no solo en métricas técnicas como los saltos.
- **Uso:** Fundamental para proveedores de servicios de Internet (ISP) y grandes redes que necesitan gestionar el enrutamiento entre diferentes dominios autónomos.

# 5. IS-IS (Intermediate System to Intermediate System)
- **Tipo:** Protocolo de estado de enlace.
- **Descripción:** Similar a OSPF, pero usa el protocolo CLNP (Connectionless Network Protocol). Se utiliza más en entornos de redes de proveedores de servicios.
- **Uso:** Menos común que OSPF, pero aún utilizado en grandes redes de telecomunicaciones y proveedores de servicios.

# 6. IGRP (Interior Gateway Routing Protocol)
- **Tipo:** Protocolo de vector de distancia.
- **Descripción:** Antiguo protocolo desarrollado por Cisco, reemplazado por EIGRP debido a sus limitaciones en cuanto a escalabilidad y eficiencia.
- **Uso:** Obsoleto en la mayoría de redes modernas, pero su versión mejorada (EIGRP) sigue siendo utilizada.

# 7. RIPng (RIP Next Generation)
- **Tipo:** Protocolo de vector de distancia.
- **Descripción:** Versión de RIP adaptada para redes IPv6. Mantiene la misma funcionalidad básica de RIP pero es compatible con el direccionamiento y características de IPv6.
- **Uso:** En redes que implementan IPv6, aunque sigue siendo más adecuado para redes pequeñas.

# 8. MPLS (Multiprotocol Label Switching)
- **Tipo:** No es un protocolo de enrutamiento en sí, pero se utiliza para acelerar el enrutamiento en redes grandes.
- **Descripción:** MPLS utiliza etiquetas para tomar decisiones de reenvío en lugar de direcciones IP, lo que permite un tráfico más rápido y eficiente. Es utilizado principalmente en redes WAN y por proveedores de servicios de Internet.
- **Uso:** Ideal para redes grandes que requieren alta velocidad y calidad de servicio, como redes empresariales y de telecomunicaciones.