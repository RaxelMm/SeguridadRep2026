# Descripcion
The numbers... what do they mean? [numbers](https://challenge-files.cylabacademy.net/library/664bc3a85525cfd5a2af151d29f2744ba334880e28e60f9a513aba13633199d4/the_numbers.png)
## Solucion
1. Abrir la imagen `the_numbers.png`.
2. Los numeros siguen el cifrado A1Z26 (A=1, B=2, ..., Z=26).
3. Convertir cada numero a su letra correspondiente:
   16=P, 9=I, 3=C, 15=O, 3=C, 20=T, 6=F
   20=T, 8=H, 5=E, 14=N, 21=U, 13=M, 2=B, 5=E, 18=R, 19=S, 13=M, 1=A, 19=S, 15=O, 14=N
4. La flag resultante es: PICOCTF{THENUMBERSMASON}
## Notas Adicionales
- **Categoria**: Cryptography -> Cifrado clasico.
- **A1Z26**: Sistema de numeracion donde cada letra del alfabeto ingles corresponde a su posicion (1-26).
- El formato de la flag es PICOCTF{...}.
- Herramientas: conversion manual, CyberChef (A1Z26), Python.
- Flag: PICOCTF{THENUMBERSMASON}
## Referencias
- picoCTF 2019 - The Numbers (Cryptography, Easy)
- Autor: Danny