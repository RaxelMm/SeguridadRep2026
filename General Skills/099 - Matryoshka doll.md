# Descripcion

## Solucion
Al descargar el archivo `tunn3l_v1s10n` y tratar de abrirlo, el visor de imágenes nos da un error. La pista *"Weird that it won't display right..."* nos sugiere que se trata de un archivo de imagen con la cabecera corrupta o maliciosa.

El proceso para repararlo y obtener la bandera fue el siguiente:

1. Al analizar los primeros bytes del archivo en un editor hexadecimal, notamos los caracteres mágicos `BM` (42 4D), lo cual indica que es un mapa de bits (archivo `.bmp`).

2. Sin embargo, algunos valores vitales en la cabecera estaban alterados:

- El **offset** (desplazamiento) donde comienzan los píxeles reales (ubicado en la posición `0x0A`) y el **tamaño de la cabecera DIB** (ubicado en la posición `0x0E`) tenían un valor de `ba d0 00 00`. El valor estándar para el offset en BMPs de 24 bits suele ser `54` (hex: `36 00 00 00`) y el tamaño de la cabecera suele ser `40` (hex: `28 00 00 00`).

3. Modificamos esos bytes usando el editor hexadecimal (o un script de Python) para restaurar los valores correctos de un BMP estándar.

4. Al hacer esta primera corrección, la imagen ya abre pero muestra un túnel cortado. El tamaño de los píxeles no coincide con el alto configurado en la cabecera.

5. El alto de la imagen (ubicado en `0x16`) indicaba `306` píxeles de alto, pero haciendo matemáticas con el peso del archivo, el alto real debía ser de `850` píxeles (hex: `52 03 00 00`).

6. Tras corregir la altura a 850 en el editor hexadecimal y guardar el archivo como `fixed.bmp`, al abrir la imagen finalmente logramos ver la imagen completa, donde la bandera aparece escrita en la parte superior del túnel que antes estaba oculta.

Bandera obtenida: `academy{qu1t3_a_v13w_2020}
## Notas Adicionales
- **Herramientas de edición hexadecimal**: Para manipular estos archivos se puede utilizar cualquier editor hexadecimal, como **HxD** en Windows, o **hexeditor** / `xxd` en distribuciones Linux. También se puede hacer mediante un pequeño script de Python usando objetos `bytearray`.

- **Estructura del formato BMP**: Este reto pone a prueba nuestro conocimiento sobre la estructura de archivos (File Signatures & File Headers). Un archivo de mapa de bits sin compresión tiene una matemática exacta: `Peso Total ≈ 54 bytes (cabecera) + (Ancho × Alto × 3 bytes)`.

- Alterar la resolución en la cabecera de la imagen sin recortar los píxeles reales es una técnica rudimentaria pero efectiva de esteganografía para esconder información visual.
## Referencias

