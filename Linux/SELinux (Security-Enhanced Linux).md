SELinux (Security-Enhanced Linux) es un sistema de control de acceso obligatorio (MAC) implementado en el kernel de Linux. Fue desarrollado originalmente por la Agencia de Seguridad Nacional de los Estados Unidos (NSA) para reforzar la seguridad en sistemas Linux al agregar un conjunto de políticas que restringen qué recursos (como archivos, dispositivos, puertos de red, etc.) pueden acceder los procesos en función de su contexto de seguridad.

SELinux opera sobre la idea de etiquetas de seguridad que se aplican tanto a los objetos (archivos, procesos, sockets, etc.) como a los sujetos (usuarios, aplicaciones) del sistema, y define qué interacciones están permitidas entre ellos a través de políticas predefinidas.

**Modos de operación de SELinux:**
1. **Enforcing**: SELinux está activo y las políticas se están aplicando. Todas las acciones no permitidas por las políticas son bloqueadas y registradas.
2. **Permissive**: SELinux está activo, pero en lugar de bloquear acciones no permitidas, solo las registra en los logs. Este modo es útil para probar configuraciones sin afectar el funcionamiento del sistema.
3. **Disabled**: SELinux está completamente deshabilitado.

# Verificar estado
```
sestatus
```

# Habilitar SELinux
Abrimos el siguiente archivo
```
sudo nano /etc/selinux/config
```

Buscamos la línea que dice **SELINUX=disabled** y cámbiala por **SELINUX=enforcing** o **SELINUX=permissive** si solo quieres probar SELinux.
```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
# enforcing - SELinux security policy is enforced.
# permissive - SELinux prints warnings instead of enforcing.
# disabled - No SELinux policy is loaded.
SELINUX=enforcing
SELINUXTYPE=targeted
```

Y después reiniciamos el sistema
```
sudo reboot
```
