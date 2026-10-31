## Descripción 
Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/bf9a20c350075c5863371e078daee1d570d4062902edc8a4a042e02a7cebf161/partition4.img.gz)
## Solución 
```
academy{71m311n3_0u7113r_h3r_43a2e7af}
```
## Notas adicionales 
* Se analizó una imagen de disco buscando archivos con marcas de tiempo adulteradas. Se utilizó `fls -m / -r partition4.img > bodyfile.txt` para volcar los metadatos de los inodos, seguido de `mactime -b bodyfile.txt > timeline.txt` para ordenarlos cronológicamente
## Referencias