---
curso dfir win4 @ 2023-06-06T14:30-16:00
curso dfir win5 @ 2023-06-08T17:00-18:00
---
# win4: artefactos


## Hive
- Rama del registro de Windows que almacena datos volátiles
- Están representadas físicamente por ficheros:
```
- \Documents and Settings\$user\NTUSER.DAT (WinXP)
- \Users\$user\NTUSER.DAT (Win7 en adelante) + \Users\$user\AppData\Local\Microsoft\Windows\UsrClass.dat
- \Windows\System32\config\DEFAULT
- \Windows\System32\config\SAM
- \Windows\System32\config\SECURITY
- \Windows\System32\config\SOFTWARE
- \Windows\System32\config\SYSTEM
```
## Shadow Copies
Desde Win7 en adelante, copias del registro cada 10 días en:
```
C:\Windows\System32\config\RegBack
```

> Recomendado para no alterar nada: navegar desde FTK Imager

- Herramienta: WRR (Windows Registry Recovery)
	- Inspección a mano
- Herramienta: RegRipper
	- Cada plugin te saca en txt algo específico

## Eventos Security Windows
- Herramienta: WinLogOnView
- Herramienta: Event Log Explorer
	- Menú "Log > Time Correction"
- Herramienta: FullEventLogView
	- Te carga todos los eventos juntos, y sobre ello puedes filtrar por tiempo

### Códigos de eventos de Windows
- 4624: An account was successfully logged on.
- 4625: An account failed to log on.
- 4776: The computer attempted to validate the credentials for an account.
	- Códigos de error según el escenario (atacante -> servidor expuesto -> DC)

## Event Trace Logs (ETL)
A partir de Win10

## USB
### Herramienta: USBDeview
### Herramienta: USB Forensic Tracker

## Prefetch
### Herramienta: WinPrefetchView

## Archivos LNK
### Herramienta: LinkParser

[..]

## Userassist
- Registra los programas con interfaz gráfica lanzados por el usuario propietario del NTUSER.dat
	- No como el prefetch, que es del sistema y no asocia ejecuciones a usuarios
- En el valor de registro
  NTUSER.dat\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{CEBFF..}\Count
  queda la lista de aplicaciones, ficheros, etc. codificados en rot13
### Herramienta: WRR
### Herramienta: RegRipper (tiene plugin Userassist)

[..]

## ShellBags
- Guarda las preferencias de visualización para cada usuario de cada carpeta.
	- Deja rastro de por qué carpetas se ha navegado. 
- C:\Users\$usuario\AppData\Local\Microsoft\Windows\UsrClass.dat
### Herramienta: toolz\ShellBagsExplorer
