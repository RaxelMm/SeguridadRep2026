## Descripción 
Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/0b369ed5974a5e777ca3bc323bd39d75a6f27762a449d16cd2a0ffc08b2a6aa8/timeline-1-partition4.img.gz)
## Solución 
```
academy{573417h13r_7h4n_7h3_1457_58527bb222}
```
## Notas adicionales 
* Mediante `fls` y `mactime`, se filtraron los archivos recién creados (`grep "macb"`) al final de la línea de tiempo MAC. Se detectó una acción anti-forense (borrado de historial y ejecución de `poweroff`) y se identificó un archivo sospechoso con fecha de creación idéntica (`/etc/chat` en el inodo 32716)
## Referencias