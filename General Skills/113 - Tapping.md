# Descripcion 
Theres tapping coming in from the wires.
## Solucion
1. Conectar al servidor con netcat para ver el mensaje:
   nc <instance>
2. El servidor muestra una secuencia de puntos (.) y guiones (-) separados por espacios.
3. Identificar que es **codigo Morse**.
4. Decodificar el mensaje Morse. Se puede usar:
   - Herramienta online: https://morsecode.world/international/translator.html
   - dCode: https://www.dcode.fr/morse-code
   - CyberChef (operacion "From Morse Code")
5. El mensaje decodificado es la flag en formato academy{}.
6. La flag obtenida es:
   academy{m0rs3_c0d3_1s_fun_88cc00f5}
## Notas Adicionales
- **Categoria**: Cryptography -> Codificacion Morse.
- **Codigo Morse**: Sistema de codificacion que usa dos simbolos (punto y guion) para representar letras y numeros. Inventado por Samuel Morse en 1830.
- Estructura:
  - Punto (.) = señal corta
  - Guion (-) = señal larga
  - Espacio = separa letras
  - Espacio triple o barra (/) = separa palabras
- Aunque se le llama "cifrado", Morse es una **codificacion** (no cifrado), porque no usa clave.
- Herramientas online usadas:
  - https://morsecode.world/international/translator.html
  - https://www.dcode.fr/morse-code
- Flag: academy{m0rs3_c0d3_1s_fun_88cc00f5}
## Referencias
- picoCTF 2019 - Tapping (Cryptography, Medium)
- Autor: Danny
- Morse translator: https://morsecode.world/international/translator.html