# lnx: forense

Recordatorios adquisición evidencias:

- Mantener el estado de la máquina.

> Si está viva, no apagar. Si está apagada, no encender.

- Adquirir en orden de mayor a menor volatilidad de la evidencia.

## Extracción en vivo de máquina vulnerada

- Usar herramientas fiables.
	- Binarios y librerías de una instalación física en pendrive de dos distros distintas.
	- El pendrive tiene cuatro particiones:
		- `/dev/sdb1`: Swap
		- `/dev/sdb2`: Caine 7 (basada en system5)
		- `/dev/sdb3`: Kali 2016.2 (basada en systemd)
		- `/dev/sdb4`: Datos (la más grande)
- Ejecución de scripts:
	- `/mnt/tools/montalo.sh                      # `
	- `./irtool01.sh /mnt/ && exit                # binarios propios, con chroot`
	- `/mnt/tools/irtool02.sh /mnt/datos/<caso1>  # binarios de la víctima`
	- `/mnt/tools/desmontalo.sh`

- En los filesystems de linux (EXT4), en vez de MFT/LogFile/Journal hay inodos.

### Pasos en máquina vulnerada

- [ ] Preparar usb con `ir_usb.7z` y pasarlo sobre `Pwned.ova` (1:07:00)

- Crear directorios `/mnt/tools/` y `/mnt/datos/`
- 
- `mount -r /dev/sdb3 /mnt/tools                    # -r: en readonly`
- `mount /dev/sdb4 /mnt/datos`
- `mkdir /mnt/datos/<caso1>`
- `mount --rbind /mnt/datos/<caso1> /mnt/tools/mnt/ # como los .sh escribirán en /mnt,
					            # monto /mnt/tools/mnt en el directorio del caso.`

- Después de ejecutar todo, asegurarse de que no hay nada cifrado que pueda corromperse y,
  si es así, tiramos del cable de corriente**
	- ** [ ] ¿por qué nos interesa tirar desconectar la corriente en este caso?
