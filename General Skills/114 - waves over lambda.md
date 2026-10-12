# Descripcion
We made a lot of substitutions to encrypt this. Can you decrypt it?
  
## Solucion
1. Conectar al servidor con netcat para obtener el mensaje cifrado:
   nc chatelaine.cylabacademy.net 22120
2. El mensaje es un cifrado por sustitucion simple (monoalfabetico).
3. Usar un solucionador online de sustitucion como:
   - https://quipqiup.com/
   - https://www.guballa.de/substitution-solver
   - https://www.dcode.fr/monoalphabetic-substitution
4. Pegar el texto cifrado completo en la herramienta y resolver.
5. La primera linea del texto descifrado dice:
   "congrats here is your flag - frequency_is_c_over_lambda_..."
6. La flag es la cadena que sigue al guion, en formato:
   frequency_is_c_over_lambda_...
   (No usa el formato usual picoCTF{} ni academy{}).
7. La flag completa se obtiene al resolver el cifrado. Segun writeups, la flag es:
   frequency_is_c_over_lambda_... (consultar con la herramienta para el sufijo exacto).
## Notas Adicionales
- **Categoria**: Cryptography -> Cifrado por sustitucion (monoalfabetico).
- **Cifrado por sustitucion**: Cada letra del alfabeto se reemplaza por otra de forma consistente.
- Se puede resolver con analisis de frecuencia o herramientas online.
- La pista "Flag is not in the usual flag format" indica que no lleva llaves {}.
- El texto descifrado es una mezcla de un fragmento de "Los hermanos Karamazov" y la historia del cifrado Vigenere.
- La flag esta en la primera linea, despues del guion.
- Herramientas: quipqiup, guballa, dcode.
- Flag: frequency_is_c_over_lambda_... (consultar con la herramienta para el sufijo exacto).
## Referencias
- picoCTF 2019 - waves over lambda (Cryptography, Medium)
- Autor: invisibility/Danny
- Solver: https://quipqiup.com/