---
curso dfir win1 @ 2023-05-09T16:30-18:00
curso dfir win1 @ 2023-05-10T15:30-16:30
---
# win1: metodología

1. Recopilación de inteligencia
2. Encontrar un punto de entrada
3. Llamar a casa
4. Búsqueda de datos/activos
5. Moverse por la red
6. Extracción de datos
[..]

## RATs
DarkCoderSc

## Elementos de una cadena de custodia
- Identificación física e inventariado de los materiales o dispositivos
	- Fotografía del entorno
	- Videograbación con fecha y hora
- Separación de los dispositivos, etiquetado y protección de los mismos (precintado)
- Documentación y registros de control. (Apertura de acta y registro de nº de serie y elementos)
- Firma del acta de los intervinientes
- Certificación de Entrada - Salida (Registro de salidas)
[..]
## Criterio de Volatilidad
1. Información de memoria -> Dump (lo que ejecutes después va a usar la memoria y la machacará)
2. Artefactos en Live (procesos, ficheros abiertos, conexiones, ARP, rutas)
3. Apagado NO ordenado de la máquina (tirar del cable de corriente)
	Si se apaga ordenadamente, se modifican/borran ficheros temporales, cachés, etc.
	Si es un disco SSD o un volumen cifrado, hacemos una adquisición de la unidad lógica en live y luego tiramos del cable.
4. Imagen/clonado de discos

## DFIRWin\Triage\EDD.exe
Detecta unidades/discos montadas y cifradas. No es 100% fiable, como cualquier otra.
Con WinTriage se puede hacer esto.
