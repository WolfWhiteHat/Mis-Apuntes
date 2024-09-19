# Modo de Red
El "modo de red" se refiere a la configuración de red que se aplica a una máquina virtual, determinando cómo se conectará la máquina virtual a la red física. Aquí hay una breve explicación de las opciones que mencionaste:

1. **Red Compartida (Shared Network):**
    - En este modo, la máquina virtual comparte la conexión a Internet del host (la máquina física, en este caso, tu Mac). La máquina virtual obtiene una dirección IP a través de NAT (Network Address Translation), lo que significa que se comunica con la red exterior a través de la dirección IP del host. Esto es útil para acceder a Internet desde la máquina virtual sin necesidad de asignar direcciones IP adicionales en la red local.
2. **VLAN Emulada (Emulated VLAN):**
    - En este modo, la máquina virtual emula una VLAN (Red de Área Local Virtual). Las VLAN son utilizadas para segmentar una red física en múltiples redes virtuales. Este modo es útil si estás trabajando con configuraciones de red más avanzadas que involucren VLAN.
3. **Solo Host (Host Only):**
    - Con esta configuración, la máquina virtual se comunica solo con el host y otras máquinas virtuales en la misma red "Solo Host". Esta opción es útil para configuraciones donde deseas que las máquinas virtuales se comuniquen entre sí, pero no tengan acceso a la red externa.
4. **Puenteada (Bridged):**
    - En modo puenteado, la máquina virtual se conecta directamente a la red física como si fuera otro dispositivo en la misma red. La máquina virtual obtiene una dirección IP propia en la red local y puede comunicarse directamente con otros dispositivos en esa red. Este modo es útil cuando necesitas que la máquina virtual sea completamente visible y accesible en la red local.


# Tarjeta de red Emulada
1. **Intel 82574L GbE Controller (e1000e):**
    - Emula un controlador Ethernet Gigabit de Intel utilizando el modelo e1000e. Se utiliza comúnmente para emular una interfaz de red Gigabit en máquinas virtuales.
2. **Intel Gigabit Ethernet (e1000):**
    - Emula un controlador Ethernet Gigabit de Intel utilizando el modelo e1000. Similar al e1000e, se utiliza para proporcionar conectividad Gigabit a las máquinas virtuales.
3. **Intel Gigabit Ethernet (e1000-82544gc):**
    - Otra variante de emulación de controlador Gigabit Ethernet de Intel. Cada variante puede tener características específicas o dirigirse a diferentes versiones de hardware.
4. **VMWare Paravirtualized Ethernet v3 (vmxnet3):**
    - Un controlador de red paravirtualizado diseñado para su uso en entornos de virtualización VMWare. Ofrece un rendimiento mejorado al interactuar directamente con la capa de virtualización.
5. **ne2k_pci:**
    - Emula una tarjeta de red NE2000 PCI. Esta emulación es compatible con máquinas virtuales que pueden requerir compatibilidad con hardware más antiguo.
6. **pcnet:**
    - Emula una tarjeta de red PCnet, que es un controlador de red compatible con NE2000 y se utiliza comúnmente en entornos de virtualización.
7. **virtio-net-device:**
    - Emulación para dispositivos virtio, una interfaz de paravirtualización diseñada para mejorar el rendimiento de las máquinas virtuales.
8. **usb-net:**
    - Emula una interfaz de red a través de USB. Puede ser útil para escenarios donde la conectividad de red se proporciona a través de dispositivos USB.
9. **tulip:**
    - Emula una tarjeta de red Tulip, que es comúnmente utilizada en entornos virtuales para proporcionar compatibilidad con hardware más antiguo.
10. **virtio-net-pci:**
    - Variante de la emulación virtio diseñada específicamente para el entorno PCI.
11. **Rocker Switch (rocker):**
    - Proporciona una emulación de interruptor de red, que se utiliza en entornos de virtualización para simular la conectividad de red compleja.
