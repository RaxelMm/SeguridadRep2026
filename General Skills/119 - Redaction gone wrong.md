  
## Descripcion
Now you DON’T see me. This report has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?
## Solucion
1. Descargar el archivo PDF proporcionado (`Financial_Report_for_ABC_Labs.pdf`).
2. Utilizar una herramienta de extracción de texto para leer el contenido del PDF, ignorando las cajas negras dibujadas encima.
   - En terminal (Linux/WSL): 
     bash
     pdftotext Financial_Report_for_ABC_Labs.pdf -

- O abrir el PDF en un navegador, seleccionar todo el texto con `Ctrl+A`, copiarlo (`Ctrl+C`) y pegarlo en un editor de texto.
    

3. El texto resaltado en negro en realidad sigue siendo seleccionable, por lo que al copiar y pegar se revelará el contenido oculto.
    
4. Buscar en el texto extraído la flag en formato `picoCTF{...}` o `academy{...}`. La flag suele estar al final del documento.
    

## Notas Adicionales

- **Categoría**: Forensics -> Análisis de PDF.
    
- **Vulnerabilidad**: Redacción inadecuada. Las cajas negras dibujadas sobre el texto (con herramientas como editores de PDF básicos) no eliminan el texto subyacente, solo lo ocultan visualmente.
    
- Una redacción correcta y segura requiere eliminar físicamente el texto del flujo de datos del PDF, no solo taparlo.
    
- **Herramientas**: `pdftotext`, `strings`, navegador web.
    

## Referencias

- picoCTF 2022 - Redaction gone wrong (Forensics, Medium)
    
- Autor: Mubarak Mikail

