---
curso dfir win2 @ 2023-05-15T09:30-13:00
curso dfir win2 @ 2023-05-17T17:00-18:00
---
# win2: adquisición de evidencias

> Si un equipo está encendido: NO APAGARLO.
-  Comparativa de herramientas de adquisición de memoria:
  https://unminioncurioso.blogspot.com/2019/02/dfir-elija-bien-su-arma-calcule-el.html
  
> Si un equipo está apagado, no encenderlo (alteraría algunos contenidos del sistema de ficheros) salvo que no quede más remedio, como por ejemplo si el disco está cifrado.

- Si la máquina es virtual, admite los dos modos: bin haciendo la adquisición en vivo o bien llevándome la memoria y discos duros desde el sistema gestor de VMs.
- Si la máquina está en la nube, solo podremos clonar en modo Live (adquisición en vivo) o llevarnos los datos (copia lógica).

En cualquier caso, lo que se debe hacer es explicar el método de adquisición en el informe pericial y justificarlo según la situación.

## Live Response
- Ejecutar como administrador

## Herramientas: RamCapturer
https://belkasoft.com/es/ram-capturer
```
C:\Users\AdministratorDesktop\Wintriage_work\Wintriage_v01032020_curso\Tools> RamCapture64.exe memoria.mem
```
Volcar la memoria es mucho más fácil en Windows que en Linux.

## Herramientas: RawCopy
Ejemplo de uso: al intentar copiar `C:\WINDOWS\system32\config\SAM`, da que el usuario SYSTEM lo tiene abierto.
RawCopy lo reintentará con un método distinto, "INDX method":
	- Copia de forma binaria lo que tenga ese fichero en el sistema de ficheros.
	- Relacionado con el índice que se guarda en el fichero `$i30` de cada directorio
	- "No pide al sistema operativo un fichero, sino que lo dumpea directamente identificando offsets desde la MFT"

## Herramientas: FTK Imager Lite
"Imprescindible, si os presentáis al examen [IRCP](https://certificaciones.securizame.com/ircp/) la usaréis sí o sí".
Si el disco está cifrado ("unrecognized file system"), solo se puede abrir como unidad lógica.

- Evitar "Esta aplicación se ha bloqueado para protegerte":
  ![[_Pasted image 20230515134738.png]]
  ![[_Pasted image 20230515134854.png]]

- AD1: AccessData (formato propietario de FTK). Para extraer los ficheros concretos que nos queremos llevar.
	- Genera `imagen.ad1.txt`, que Lorenzo siempre adjunta como Anexo 2 (el Anexo 1 es su CV) al informe pericial.
