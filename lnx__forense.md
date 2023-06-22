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
	- `montalo.sh`
	- `irtool01.sh`
	- `irtool02.sh`
	- `desmontalo.sh`

- En los filesystems de linux (EXT4), en vez de MFT/LogFile/Journal hay inodos.

### Pasos en máquina vulnerada

- Crear directorios `/mnt/tools/` y `/mnt/datos/`
- 
- `mount -r /dev/sdb3 /mnt/tools                           # -r: en readonly`
- `mount /dev/sdb4 /mnt/datos`
- `mkdir /mnt/datos/<nombre_caso>`
- `mount --rbind /mnt/datos/<nombre caso> /mnt/tools/mnt/` # como los .sh escribirán en /mnt,
							   # monto /mnt/tools/mnt en el directorio
 							   # del caso.
