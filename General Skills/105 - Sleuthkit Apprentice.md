# Descripcion
Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://challenge-files.cylabacademy.net/library/162bc8bf6dd1abbc5269c16570e170277369a39cf46bdd8d99443e136fabcc5f/disk.flag.img.gz)
## Solucion
1. Mover el archivo a /tmp para evitar problemas de espacio:
   cp ~/disk.flag.img.gz /tmp/
2. Ir a /tmp y descomprimir:
   cd /tmp
   gunzip disk.flag.img.gz
3. Listar la tabla de particiones con mmls:
   mmls disk.flag.img
   Identificar el Start de la particion Linux (por ejemplo 360448).
4. Listar recursivamente los archivos de la particion:
   fls -o 360448 -r disk.flag.img
   Salida:
   r/r 2363:       .ash_history
   d/d 3981:       my_folder
   + r/r * 2082(realloc):  flag.txt
   + r/r 2371:     flag.uni.txt
5. Extraer el contenido del archivo flag.uni.txt con icat, usando su inodo (2371):
   icat -o 360448 disk.flag.img 2371
6. La flag aparece en la salida:
   academy{by73_5urf3r_85e9b307}
## Notas Adicionales
- **Categoria**: Forensics -> analisis de imagenes de disco.
- `mmls` muestra la tabla de particiones. La columna `Start` es el offset en sectores que se pasa con `-o` a los demas comandos de Sleuth Kit.
- `fls -r -o <offset>` lista los archivos de forma recursiva, mostrando el inodo, el tipo (r=regular, d=directorio) y el nombre.
- El asterisco `*` antes del inodo indica un archivo eliminado (realloc). Se puede recuperar con icat.
- `icat -o <offset> <img> <inodo>` extrae el contenido de un archivo por su inodo.
- Errores comunes:
  - Poner el offset como argumento posicional: `fls disk.img 360448` (mal). El offset va con `-o`: `fls -o 360448 disk.img`.
  - Confundir el inodo (numero antes de los dos puntos) con el nombre.
- Herramientas: mmls, fls, icat (Sleuth Kit), gunzip.
- Flag: academy{by73_5urf3r_85e9b307}
## Referencias
- picoCTF 2022 - Sleuthkit Apprentice (Forensics, Medium)
- Autor: LT 'syreal' Jones
- Sleuth Kit: https://www.sleuthkit.org/

