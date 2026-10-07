# Descripcion
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image. [dds1-alpine.flag.img.gz](https://challenge-files.cylabacademy.net/library/0e33413e7b309ae38964211ca09f5c86005b6fe4f2cc95b75ad5b482d98a2d76/dds1-alpine.flag.img.gz)

## Solucion
1. Verificar los archivos disponibles:
   ls -la
2. Descomprimir el archivo .gz SIN crear archivo en disco (problema de espacio):
   zcat dds1-alpine.flag.img.gz | strings | grep -o "picoCTF{[^}]*}"
   O alternativamente:
   gunzip -c dds1-alpine.flag.img.gz | strings | grep -i "picoCTF\|academy"
3. La flag aparece en la salida del comando.
## Notas Adicionales
- **Categoria**: Forensics -> analisis de imagenes de disco.
- El webshell tiene espacio limitado, por lo que gunzip directo falla con "No space left on device".
- Solucion: usar zcat o gunzip -c para descomprimir en streaming sin escribir a disco.
- strings extrae cadenas ASCII imprimibles del binario.
- grep -o "picoCTF{[^}]*}" extrae solo el patron de la flag.
## Referencias

