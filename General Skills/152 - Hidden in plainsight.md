## Descripción 
You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag. Download the jpg image [here](https://challenge-files.cylabacademy.net/library/90fe779e0989ed7c80652fdd2b165f9661a7a00ba75fc766d01cd4c0e489fdbd/img.jpg).
## Solución 
```
academy{h1dd3n_1n_1m4g3_7ba83d11}
```
## Notas adicionales 
* Al igual que con los documentos PDF, se utilizó la herramienta `exiftool` en la terminal para extraer y analizar los datos EXIF de la imagen JPG. La bandera se encontraba inyectada como un payload oculto dentro de los campos de los metadatos del archivo
## Referencias