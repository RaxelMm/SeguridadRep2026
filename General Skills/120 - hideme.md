## Descripcion
Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here.
## Solución
En este reto de esteganografía y análisis forense se nos entrega una imagen llamada `flag.png`. La descripción nos insinúa que hay "más de lo que se ve a simple vista" (*more than what meets the eye*).

1. Al examinar los bytes del archivo `flag.png`, se detecta la firma mágica `PK\x03\x04` a partir del offset `15929`, lo que indica la presencia de un archivo ZIP incrustado al final de la imagen PNG original.
2. Al descomprimir el archivo ZIP (o extraer su contenido), se encuentra una carpeta llamada `secret/` que contiene una segunda imagen `flag.png`.
3. Al inspeccionar la imagen oculta (o buscar cadenas de texto dentro de ella), se obtiene la bandera del reto.

Bandera obtenida: `academy{Hiddinng_An_imag3_within_@n_ima9e_404ff71e}`

## Notas Adicionales
- **Resolución con Binwalk / Foremost (Linux)**: 
  - Puedes verificar y extraer el contenido oculto directamente con `binwalk -e flag.png` o usando `foremost flag.png`.
  - La herramienta generará una carpeta con el archivo ZIP extraído y la carpeta `secret/flag.png`.
- **Resolución con 7-Zip / Scripts**:
  - En Windows, al estar concatenado un archivo ZIP al final del PNG, muchas veces se puede abrir directamente haciendo clic derecho en `flag.png` > *Abrir con 7-Zip* o utilizando un script en Python con la librería `zipfile`.
- **Técnica de esteganografía**: Concatenación de archivos (*file appending*). Dado que los visores de imágenes leen hasta el bloque de fin de archivo (`IEND` en PNG), cualquier información agregada después del final suele ser ignorada por el visor pero permanece intacta en el archivo.

## Referencias
- [Binwalk - Herramienta de análisis de firmas y extracción](https://github.com/ReFirmLabs/binwalk)
- [Estructura del formato PNG (W3C)](https://www.w3.org/TR/png/)
- [List of File Signatures / Magic Bytes](https://en.wikipedia.org/wiki/List_of_file_signatures)