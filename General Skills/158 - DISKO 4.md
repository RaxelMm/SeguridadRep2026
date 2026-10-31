## Descripción 
Can you find the flag in this disk image? This time I deleted the file! Let see you get it now! Download the disk image [here](https://challenge-files.cylabacademy.net/library/73410159cc8aafa59ec856dcc13ab8b30a50f6827eef6627d3e346bbd3c0085a/disko-4.dd.gz)
## Solución 
```
academy{d3l_d0n7_h1d3_w3ll_9748d144}
```
## Notas adicionales 
* Al ejecutar `fls -d -r imagen.dd`, se detectaron dos archivos eliminados, destacando `dont-delete.gz` en el inodo 532021. Para recuperar y leer este archivo comprimido en un solo paso, se concatenaron `icat` y `zcat` mediante el comando `icat disko-4.dd 532021 | zcat`, revelando la bandera oculta
## Referencias