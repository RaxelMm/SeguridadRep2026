# Descripcion
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?
## Solución

El reto "CanYouSee" nos proporciona un archivo comprimido `unknown.zip`. Las pistas sugieren revisar la información/metadatos de la imagen (*"How can you view the information about the picture?"*) y prestar atención a datos con formatos inusuales (*"If something isn't in the expected form..."*).

1. Descomprimimos `unknown.zip`, obteniendo la imagen `ukn_reality.jpg`.

2. Analizamos los metadatos de la imagen (usando herramientas como `exiftool` o inspeccionando los metadatos XMP).

3. Dentro del campo de metadatos `Attribution URL` (`cc:attributionURL`), encontramos una cadena codificada en Base64 en lugar de una URL normal:

   text

   YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI2NmRlMWV9Cg==

4. Decodificamos la cadena Base64 para obtener la bandera en texto plano:
    
    bash
    
    echo "YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI2NmRlMWV9Cg==" | base64 -d
    

Bandera obtenida: `academy{ME74D47A_HIDD3N_9266de1e}`

## **Notas Adicionales**

- **Uso de ExifTool en Linux / Terminal**:
    - Al ejecutar `exiftool ukn_reality.jpg`, uno de los campos mostrados es:
        
        text
        
        Attribution URL                 : YWNhZGVteXtNRTc0RDQ3QV9ISUREM05fOTI2NmRlMWV9Cg==
        
    - Se puede extraer y decodificar directamente en una sola línea:
        
        bash
        
        exiftool -AttributionURL -b ukn_reality.jpg | base64 -d
        
- **Metadatos XMP en imágenes**: Los archivos JPEG no solo almacenan etiquetas EXIF estándar, sino también metadatos XMP (Extensible Metadata Platform) basados en XML, utilizados frecuentemente para derechos de autor, licencias y autoría (Creative Commons).
- **Técnica forense**: La manipulación de metadatos es una técnica común para ocultar información sin alterar la apariencia visual ni la integridad del archivo multimedia.

## **Referencias**

- [ExifTool by Phil Harvey](https://exiftool.org/)
- [Adobe XMP (Extensible Metadata Platform) Overview](https://es.wikipedia.org/wiki/Extensible_Metadata_Platform)
- [Base64 Encoding & Decoding Reference](https://es.wikipedia.org/wiki/Base64)
