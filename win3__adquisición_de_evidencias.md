---
curso dfir win3 @ 2023-05-25T16:00-18:00
curso dfir win3 @ 2023-05-29T13:30-15:00
---
# win3: adquisición de evidencias

## Herramientas: LastActivityView
## Herramientas: Winaudit
## Herramientas: Win-UFO
Incluido en CAINE hasta 7 (ahora vamos por la 11)
	- Va en una partición de solo lectura, para Live USBs (lo podrías conectar a un equipo infectado con ransomware y no le pasaría nada). Si te quieres llevar algo, tendrás que enchufar otro dispositivo de escritura.
	- No viene en las herramientas dentro de `DFIRWin/`.
## Herramientas: IRTriage
- En "Evidence Collection", vemos que no saca el JOURNAL de Windows.
- Saca los VSCs (Volume Shadow Copies), aunque por defecto viene deshabilitado.
## Herramientas: Windows Live Response
[..]
> Si nos conectamos a la víctima por RDP,
> podemos activar en "Local Resources > More" el mapeado de nuestra unidad C:,
> de forma que podamos ejecutar allí nuestras herramientas contaminando la víctima lo menos posible.
> - El ejecutable (por ejemplo, FTK o WindowsLiveResponse) y sus DLLs se cargan en la máquina destino.
> 	- [x] #to-do "Run as administrator" necesitará admin de la víctima, ¿no? ¿Qué hacemos si no lo tenemos?

## Herramientas: WMIC
En una cmd, después de ejecutar `wmic` (o si no `wmic + comando`):
```
product get name,version
```
```
wmic:root\cli>process call create "notepad.exe"
```
```
wmic:root\cli>/node:localhost /user:$user /password:$pass process where name="paint.exe" call terminate
```

## Clonado de discos
No es lo mismo clonar un disco que hacerle una imagen:
- Clonado: es bit a bit. Recomendable que el disco destino sea más grande.
	- Los hashes van a cambiar. Solo coincidirían si los discos fueran idénticos bit a bit (que nunca lo son).
- Imagen: Se hace de disco o volumen a un sistema de ficheros.

### Software
Lorenzo no tiene clonadora física. Usa:
- Distribución forense (CAINE)
- Guyimager
- 2 conectores USB 3.0 + RJ-45 1Gbps
- Disco duro externo con espacio suficiente (USB 3.0)
- Dock tipo Icy Box

## Tipos de adquisición
### Indirecta
- Extracción del disco original
- Clonado (ya sea hardware o software)
### Directa
- Usando distribución Linux LiveUSB y...
	- Antes de arrancar, buscar "boot order [marca/modelo del ordenador en cuestión]"
- ...y usando el hardware del ordenador:
	- Ej: Con RAID-5 (3 o más discos) o RAID-0 (nada redundado)

### Herramientas de clonado: Guymager
Sobre el disco nuevo insertado, "Acquire image":
	- Podemos elegir formato .dd o .exx (formato propietario de EnCASE)
	- En "Image filename" y "Info filename", recomienda poner el núm. de serie del disco.
Lorenzo suele anexar el .info resultante al informe.

### Formatos de imágenes
- RAW (con `dd`): evidencia pura, sin metadatos
- EWF/E01: el de EnCASE
	- Comprime, particiona, tiene metadatos
- AFF: formato opensource
	- Comprime, particiona, tiene metadatos
- Discos virtuales:
	- VMDK (VMWare)
	- VDI (VirtualBox)
	- VHD/VHDX (Microsoft Hyper-V)
		- Convertir a VHD puede que nos haga falta para ver las shadow copies.
- Con 7zip se puede ver el sistema de ficheros de un .vdi o de un .vmdk

### Autopsy
- Timeline

### Montaje de imágenes
```
mount -t sistema_de_ficheros -o opciones imagen.dd /mnt/destino
opciones: ro loop offset [show_sys_files streams_interface=windows]{si NFTS}
```

### Búsqueda de ficheros: [Everything](https://www.voidtools.com/downloads)
- Portable, indexa muy rápido y permite buscar patrones (en la MFT).
