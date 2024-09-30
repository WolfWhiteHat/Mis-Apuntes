**RustScan** es una herramienta de escaneo de puertos extremadamente rápida, diseñada para mejorar la velocidad en la detección de puertos abiertos en una red. Su principal ventaja es que combina la velocidad de **Rust** (un lenguaje de programación muy eficiente) con la flexibilidad de **Nmap**. Mientras que herramientas tradicionales como Nmap son muy completas pero pueden ser lentas en grandes redes, RustScan optimiza la etapa de descubrimiento de puertos y luego utiliza Nmap para realizar un escaneo más profundo.

```
https://github.com/RustScan/RustScan
```


# Instalacion
```
wget https://github.com/RustScan/RustScan/releases/download/2.3.0/rustscan-2.3.0-aarch64-macos.tar.xz
```

# Descarga de paquetes
```
sudo dpkg -i rustscan-2.3.0-aarch64-macos.tar.xz
```

# Descarga de dependencias
```
sudo apt --fix-broken install
```

# Vericar instalación
```
rustscan --version
```

