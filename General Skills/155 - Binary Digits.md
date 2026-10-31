## Descripción 
This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this? Download the file [here](https://challenge-files.cylabacademy.net/library/819e05da202722f7847eab5c0efdedc194be8a2bc19e6b436d057c8514ae70bc/digits.bin).
## Solución 
```
academy{h1dd3n_1n_th3_b1n4ry_5a7375c5}
```
## Notas adicionales 
* El archivo contenía texto ofuscado mediante codificación binaria directa (caracteres `1` y `0`). Se procesó la cadena agrupando los dígitos en bloques de 8 bits para convertirlos de base 2 a caracteres ASCII, revelando el texto plano y la bandera oculta
## Referencias