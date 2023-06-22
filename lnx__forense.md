# lnx: forense

Recordatorios adquisición evidencias:

- Mantener el estado de la máquina.

> Si está viva, no apagar. Si está apagada, no encender.

- Adquirir en orden de mayor a menor volatilidad de la evidencia.

## Extracción en vivo de máquina vulnerada

- Usar herramientas fiables.
	- Binarios y librerías de una instalación física en pendrive de dos distros distintas.
	- El pendrive tiene cuatro particiones:
		- Swap
		- Caine 7 (basada en system5)
		- Kali 2016.2 (basada en systemd)
		- Datos (la más grande)
- Ejecución de scripts:
	- `montalo.sh`
	- `irtool01.sh`
	- `irtool02.sh`
	- `desmontalo.sh`
