## Descripción 
This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file [here](https://challenge-files.cylabacademy.net/library/cefad24659aa422bb4e57016eda1c098a0e8f3e83fbf006b58c235ca0440cb9e/file)
## Solución 
```
academy{r3st0r1ng_th3_by73s_d28873c8}
```
## Notas adicionales 
* El archivo carecía de extensión y estaba dañado por tener su encabezado hexadecimal (Magic Bytes) alterado. Sabiendo que era un JPEG, se inspeccionó con `xxd` y se parchearon los primeros 4 bytes del archivo para restaurar la firma estándar `FF D8 FF E0`. Tras guardar los cambios, la imagen volvió a ser legible y reveló la bandera visualmente
## Referencias