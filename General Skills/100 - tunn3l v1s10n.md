# Descripcion
We found this file. Recover the flag. [tunn3l_v1s10n
## Solucion
Para este reto de esteganografía se nos proporciona una imagen (`dolls.jpg`). Tal como la descripción lo insinúa (haciendo alusión a las famosas muñecas rusas "Matrioshkas" que se guardan una dentro de la otra), este archivo esconde múltiples capas de archivos incrustados en su interior.

El proceso para encontrar la bandera consistió en pelar estas capas:

1. Al analizar el código binario de la imagen original (`dolls.jpg`), descubrimos que contenía un archivo ZIP concatenado al final.

2. Al extraer este primer ZIP, obtuvimos una nueva imagen llamada `2_c.jpg`.

3. Repetimos el mismo procedimiento con esta nueva imagen, ya que también ocultaba otro archivo ZIP en su interior. Al extraerlo, nos dio la imagen `3_c.jpg`.

4. Continuamos el proceso una vez más y encontramos la imagen `4_c.jpg` anidada.

5. Al analizar y extraer el ZIP oculto dentro de la última imagen (`4_c.jpg`), finalmente hallamos un archivo de texto llamado `flag.txt`. Al leerlo, contenía nuestra bandera.

Bandera obtenida: `academy{ZNTyvSDXRNO1d0xCkBRMhAoiafpCTvgW}`
## Notas Adicionales
## Referencias

