
## Descripcion
Files can always be changed in a secret way. Can you find the flag? cat.jpg
## Solucion
1. Descargar la imagen `cat.jpg`.
2. Revisar los metadatos (EXIF) del archivo. Se puede usar:
   - Terminal: `exiftool cat.jpg`
   - Terminal: `strings cat.jpg | grep -i "license\|pico\|academy"`
   - Online: https://jimpl.com/ o cualquier visor de EXIF.
3. En el campo **License** (o Copyright) aparece una cadena codificada en Base64:
   `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`
4. Decodificar la cadena en Base64:
   bash
   echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d

Resultado: `picoCTF{the_m3tadata_1s_modified}`

5. Cambiar el prefijo `picoCTF` por `academy` (segun la pista).
    
6. La flag final es: `academy{the_m3tadata_1s_modified}`
    

## Notas Adicionales

- **Categoria**: Forensics -> Analisis de metadatos.
    
- **EXIF**: Metadatos insertados en imagenes (camara, fecha, software, licencia).
    
- Los metadatos se pueden modificar facilmente (ej. con `exiftool -License="..."`).
    
- Herramientas: `exiftool`, `strings`, `base64 -d`, visores EXIF online.
    

## Referencias

- picoCTF 2021 - information (Forensics, Easy)
    
- Autor: susie