# Descripcion
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?
## Solución
El reto "Secret of the Polyglot" nos entrega un archivo llamado `flag2of2-final.pdf`. El término *polyglot* (políglota) en informática y seguridad hace referencia a un archivo válido en dos o más formatos simultáneamente.

1. **Inspección de firmas**: Al analizar los primeros bytes del archivo `flag2of2-final.pdf`, detectamos la firma mágica de una imagen PNG (`\x89PNG\r\n\x1a\n`), a pesar de tener extensión `.pdf`. Más adelante en el archivo, se encuentra la cabecera estándar de un documento PDF (`%PDF-1.4`).
2. **Parte 1 (Visualización como PNG)**:
   - Al cambiar la extensión a `.png` o abrir el archivo con un visor de imágenes, se visualiza la primera mitad de la bandera:
     ```text
     academy{f1u3n7_
     ```
3. **Parte 2 (Visualización como PDF)**:
   - Al abrir el archivo con un lector de PDF (o descomprimir sus flujos de texto internos `FlateDecode`), el documento renderiza la segunda mitad de la bandera:
     ```text
     1n_pn9_&_pdf_96385309}
     ```
4. **Unión de partes**: Combinando ambas mitades obtenemos la bandera completa:
   `academy{f1u3n7_1n_pn9_&_pdf_96385309}` ("*fluent in png & pdf*").

Bandera obtenida: `academy{f1u3n7_1n_pn9_&_pdf_96385309}`

## Notas Adicionales
- **¿Qué es un archivo políglota?**: Es un archivo diseñado para que los analizadores (*parsers*) de distintos tipos de formatos lo interpreten como válido sin generar errores. Los visores de imágenes PNG leen hasta encontrar el fragmento `IEND`, ignorando lo que haya después, mientras que los visores de PDF buscan su cabecera y tabla xref/trailer dentro del archivo ignorando bytes iniciales extraños.
- **Resolución rápida en Linux**:
  - Para ver la primera parte: `cp flag2of2-final.pdf flag.png && xdg-open flag.png`
  - Para ver la segunda parte: `pdftotext flag2of2-final.pdf -` o abriéndolo directamente en un visor de PDF.

## Referencias
- [PoC||GTFO - Polyglot Files Explanation & Examples](https://github.com/angea/pocorgtfo)
- [PNG Specification - Chunk structure](https://www.w3.org/TR/png/#5DataRep)
- [Adobe PDF Reference - File Structure](https://opensource.adobe.com/dc-acrobat-sdk-docs/pdfstandards/PDF32000_2008.pdf)