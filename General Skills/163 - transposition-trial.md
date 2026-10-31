## Descripción 
orrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message [here](https://challenge-files.cylabacademy.net/library/c432352dd1b936c7ab4ceb162b63dafa1292c57462d832c59614d4db0de130be/message.txt).
## Solución 
```
academy{7R4N5P051N6_15_3XP3N51V3_5571D3F8}
```
## Notas adicionales 
* Se elaboró un script en Python que itera el archivo en saltos de 3 índices, reordenando cada bloque mediante la lógica `bloque[2] + bloque[0] + bloque[1]` para ensamblar el texto plano y revelar la bandera.
## Referencias