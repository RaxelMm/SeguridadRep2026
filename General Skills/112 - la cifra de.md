# Descripcion
I found this cipher in an old book.
## Solucion
1. Conectar al servidor con netcat para obtener el mensaje cifrado:
   nc chatelaine.cylabacademy.net 39204
2. Identificar el cifrado. El titulo "la cifra de" hace referencia a Blaise de Vigenere.
   El texto conserva espacios y solo contiene letras, caracteristicas del cifrado Vigenere.
3. Usar el solucionador online de Vigenere: https://www.guballa.de/vigenere-solver
4. Pegar el texto cifrado completo en el campo "Cipher Text".
5. Dejar la configuracion por defecto:
   - Cipher Variant: Classical Vigenere
   - Language: English
   - Key Length: 3-30
6. Presionar "Start". La herramienta encuentra la clave "flag" automaticamente.
7. El cleartext descifrado contiene la flag en una de las lineas:
   academy{b311a50_0r_v1gn3r3_c1ph3r623c515c}
8. Enviar la flag en el formato academy{...}.
## Notas Adicionales
- **Categoria**: Cryptography -> Cifrado Vigenere (polialfabetico).
- **Vigenere**: Cifrado que usa una palabra clave para aplicar diferentes desplazamientos
  Cesar a cada letra. Fue considerado indescifrable por siglos.
- El titulo "la cifra de" es una referencia al libro "La cifra del Sig. Giovan Battista Bellaso"
  publicado en 1553, donde se describio por primera vez el cifrado.
- La clave utilizada en este reto es "flag".
- El texto descifrado habla sobre la historia del cifrado Vigenere y las atribuciones erroneas
  que recibio Blaise de Vigenere (quien no lo invento, solo lo popularizo).
- La flag esta escondida en una de las lineas del texto descifrado.
- **Error comun**: confundir la "b" con una "m" al leer la flag en la salida de la herramienta.
- Herramientas online:
  - https://www.guballa.de/vigenere-solver (usada en este reto)
  - https://www.dcode.fr/vigenere-cipher
  - CyberChef (operacion Vigenere Decode)
- Flag: academy{b311a50_0r_v1gn3r3_c1ph3r623c515c}
## Referencias
- picoCTF 2019 - la cifra de (Cryptography, Medium)
- Autor: Alex Fulton/Daniel Tunitis
- Solver usado: https://www.guballa.de/vigenere-solver