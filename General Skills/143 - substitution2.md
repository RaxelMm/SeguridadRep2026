# Descripcion
It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher? Download the message [here](https://challenge-files.cylabacademy.net/library/750a77d87fa924d5ec8a173d7354dd57792a1597cab3d89fa7443608ba0a35e7/message.txt).
## Solución
El reto "substitution2" nos presenta un texto cifrado mediante un **cifrado por sustitución monoalfabética**, pero sin espacios ni signos de puntuación (un flujo continuo de texto). La pista sugiere realizar un análisis de grupos de letras (*n-gramas*).
1. **Análisis de n-gramas y cribado de la bandera**:
   - Al final del texto cifrado encontramos la estructura de la bandera:
     ```text
     ...xclimrtgureroljb{A6S4J_4A41B515_15_73O10V5_IO56E357}
     ```
   - Analizando el prefijo justo antes de la llave `{`:
     - El trigrama más repetido en todo el texto es `xcl` (19 veces), que corresponde a la palabra más común en inglés: `the` (`x` $\rightarrow$ `t`, `c` $\rightarrow$ `h`, `l` $\rightarrow$ `e`).
     - `imrt` corresponde a `flag` (`i` $\rightarrow$ `f`, `m` $\rightarrow$ `l`, `r` $\rightarrow$ `a`, `t` $\rightarrow$ `g`).
     - `gu` corresponde a `is` (`g` $\rightarrow$ `i`, `u` $\rightarrow$ `s`).
     - `reroljb` tiene la 1.ª y 3.ª letra idéntica (`r` $\rightarrow$ `a`), coincidiendo exactamente con el formato `academy`:
       - `r` $\rightarrow$ `a`, `e` $\rightarrow$ `c`, `o` $\rightarrow$ `d`, `l` $\rightarrow$ `e`, `j` $\rightarrow$ `m`, `b` $\rightarrow$ `y`.
2. **Descifrado del interior de la bandera**:
   - Mapeamos las letras mayúsculas del contenido `{A6S4J_4A41B515_15_73O10V5_IO56E357}`:
     - `A6S4J` $\rightarrow$ **`N6R4M`** (*NGRAM*)
     - `4A41B515` $\rightarrow$ **`4N41Y515`** (*ANALYSIS*)
     - `15` $\rightarrow$ **`15`** (*IS*)
     - `73O10V5` $\rightarrow$ **`73D10U5`** (*TEDIOUS*)
     - `IO56E357` $\rightarrow$ **`FD56C357`** (sufijo hexadecimal: `I` $\rightarrow$ `F`, `O` $\rightarrow$ `D`, `E` $\rightarrow$ `C`)
   - El mensaje en *leetspeak* dice: *"NGRAM ANALYSIS IS TEDIOUS"* seguido del identificador hexadecimal.
Bandera obtenida: `academy{N6R4M_4N41Y515_15_73D10U5_FD56C357}`
## Notas Adicionales
- **Script en Python para descifrar la bandera**:
  `python`
  `flag_ct = "A6S4J_4A41B515_15_73O10V5_IO56E357"`
  `char_map = {`
      `"A": "N",`
      `"S": "R",`
      `"J": "M",`
      `"B": "Y",`
      `"O": "D",`
      `"V": "U",`
      `"I": "F",`
      `"E": "C",`
  `}`
  `decoded_flag = "".join(char_map.get(ch, ch) for ch in flag_ct)`
  `print(f"academy{{{decoded_flag}}}")`
Importancia de los N-gramas sin puntuación: Cuando un texto no tiene delimitadores de palabras (espacios o puntuación), el criptoanálisis se basa en las frecuencias estadísticas de monogramas (letras individuales), diagramas (th, he, in, er) y trigramas (the, and, ing, ion) para reconstruir la clave sin ambigüedades.
Herramientas automáticas: Solucionadores automáticos basados en algoritmos de ascenso de colina (hill-climbing) como quipqiup.com
 o guballa.de/substitution-solver
 son capaces de segmentar y resolver textos continuos sin espacios.
## Referencias
Análisis de N-gramas en Criptoanálisis (Wikipedia)
Guballa Substitution Solver - Cifrados sin espacios
Frecuencias de letras y n-gramas en el idioma inglés