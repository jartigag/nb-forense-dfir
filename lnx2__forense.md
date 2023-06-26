# lnx2: forense en la nube, ram

- Crear dos recursos NFS o SMB en sitio "conocido" (nube restringida por nosotros): IR (read-only) y Datos (read-write)
- Permitir acceso remoto desde máquina afectada (reglas en FW y NAT entrante)
- Montaje previo de recurso IR en `/mnt/nfs`
- Montaje de recurso read-write en `/mnt/datos`
- Montaje de `/mnt/tools`
  `mount -o loop,offset=$((4196352*512)),noload /mnt/nfs/ ir_lnx_usb.dd /mnt/tools/ # para systemV`
  `mount -o loop,offset=$((25167872*512)),noload /mnt/nfs/ ir_lnx_usb.dd /mnt/tools/ # para systemD`
