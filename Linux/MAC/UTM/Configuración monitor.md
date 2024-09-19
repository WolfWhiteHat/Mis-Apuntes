# Tarjetas gráficas emuladas
1. **Cirrus CLGD 54xx VGA (cirrus-vga):** Este es un emulador de una tarjeta gráfica VGA basada en el chipset Cirrus Logic GD 54xx. Es comúnmente utilizado en máquinas virtuales para sistemas operativos antiguos.
    
2. **Serial Graphics Adapter (sga):** Esta tarjeta emula un adaptador gráfico simple que utiliza la salida serial para mostrar información gráfica. Puede ser útil en entornos donde la emulación gráfica completa no es necesaria.
    
3. **Spice QXL GPU (primary, vga compatible) (qxl-vga):** El Spice QXL GPU es un controlador gráfico para máquinas virtuales que se utiliza con el protocolo de visualización SPICE. Proporciona una experiencia de visualización mejorada y rendimiento gráfico en comparación con algunas tarjetas gráficas más simples.
    
4. **Spice QXL GPU (secondary) (qxl):** Similar al anterior, pero funciona como una tarjeta gráfica secundaria.
    
5. **VGA:** La emulación estándar de una tarjeta gráfica VGA, que es compatible con una amplia gama de sistemas operativos y aplicaciones.
    
6. **ati-vga:** Emulador de una tarjeta gráfica VGA compatible con la tecnología de ATI.
    
7. **bochs-display:** Bochs es un emulador de máquina x86, y esta tarjeta gráfica emulada permite la visualización de salida gráfica.
    
8. **isa-cirrus-vga:** Una versión de la emulación de la tarjeta Cirrus VGA que se conecta al bus ISA (Industry Standard Architecture).
    
9. **isa-vga:** Emulación estándar de una tarjeta gráfica VGA conectada al bus ISA.
    
10. **ram framebuffer standalone device (ramfb):** Una tarjeta gráfica simple que utiliza la memoria RAM como un framebuffer independiente.
    
11. **secondary-vga:** Emula una segunda tarjeta gráfica VGA.
    
12. **virtio-gpu-device:** Virtio es un estándar para dispositivos de virtualización. Esta tarjeta gráfica virtio se utiliza para mejorar el rendimiento gráfico en máquinas virtuales.
    
13. **virtio-gpu-gl-device (GPU Supported):** Similar a virtio-gpu-device, pero con soporte adicional para OpenGL.
    
14. **virtio-gpu-gl-pci (GPU Supported):** Versión de la tarjeta gráfica virtio con soporte para OpenGL y conectada al bus PCI.
    
15. **virtio-gpu-pci:** Otra variante de la tarjeta gráfica virtio conectada al bus PCI.
    
16. **virtio-ramfb:** Una variante de la tarjeta virtio que utiliza un framebuffer en la memoria RAM.
    
17. **virtio-ramfb-gl (GPU Supported):** Similar a virtio-ramfb pero con soporte adicional para OpenGL.
    
18. **virtio-vga:** Otra implementación de una tarjeta gráfica virtio para mejorar el rendimiento gráfico en máquinas virtuales.
    
19. **virtio-vga-gl (GPU Supported):** Variante de virtio-vga con soporte adicional para OpenGL.
    
20. **vmware-svga:** Emulador de la tarjeta gráfica utilizada por VMware, diseñada para funcionar con máquinas virtuales en entornos VMware.