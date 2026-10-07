# Descripcion
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

[Download disk image](https://challenge-files.cylabacademy.net/library/d8718cbbc14dcd9f9aad532a51d7a01b00e1715ca3b1d654dfef687d0b15cbf5/disk.img.gz)
  
## Solucion
1. Mover el archivo descargado a /tmp (evitar problemas de espacio en home):
   cp ~/XDDDDDDDDDDDD/disk.img.gz /tmp/
2. Ir a /tmp y descomprimir:
   cd /tmp
   gunzip disk.img.gz
3. Analizar la imagen de disco con mmls:
   mmls disk.img
4. Salida del comando:
   DOS Partition Table
   Offset Sector: 0
   Units are in 512-byte sectors
         Slot      Start        End          Length       Description
   000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
   001:  -------   0000000000   0000002047   0000002048   Unallocated
   002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
5. Anotar el tamano de la particion Linux: Length = 202752 sectores.
6. Conectar al checker remoto:
   nc chatelaine.cylabacademy.net 14288
7. Introducir 202752 como respuesta.
8. El checker devuelve la flag.
## Notas Adicionales
- **Categoria**: Forensics -> analisis de imagenes de disco.
- `mmls` (Sleuth Kit) muestra la tabla de particiones de una imagen de disco.
- La columna `Length` es el tamano en sectores de 512 bytes.
- Si el checker pide bytes en lugar de sectores: 202752 * 512 = 103809024.
- El webshell tiene espacio limitado en home, por eso se debe usar /tmp.
- Errores comunes:
  - No usar /tmp y quedarse sin espacio al descomprimir.
  - Confundir Start/End con Length (Length es el tamano correcto).
- Herramientas: mmls, gunzip, nc (netcat).
- Flag: picoCTF{mm15_f7w!} (o academy{...} en CyLab).

## Referencias
