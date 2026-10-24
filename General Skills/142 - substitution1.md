# Descripcion
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again. Download the message [here](https://challenge-files.cylabacademy.net/library/2b9afd354b9804667c07bd1cddecd56fa43db5878bca2dbe74c87dff1344e5c6/message.txt).
## Solución
El reto "substitution1" nos entrega un mensaje cifrado mediante un **cifrado por sustitución monoalfabética**, pero a diferencia de la versión anterior, no incluye la clave explícita al inicio. Las pistas nos sugieren realizar un **análisis de frecuencias** (*frequency attack*) y apoyarnos en la puntuación y palabras individuales.
1. **Análisis de palabras clave y frecuencias**:
   - Observando la primera frase del texto:
     ```text
     RZFt (tquvz fuv rlwzbvp zqp felg) lvp l zcwp uf ruawbzpv tprbvnzc ruawpznznuo.
     ```
   - Reconocemos inmediatamente la definición habitual en competiciones de seguridad informática:
     ```text
     CTFs (short for capture the flag) are a type of computer security competition.
     ```
   - Esto nos proporciona directamente la equivalencia de la mayoría de las letras del abecedario:
     - `r` $\rightarrow$ `c`, `z` $\rightarrow$ `t`, `f` $\rightarrow$ `f`, `t` $\rightarrow$ `s`
     - `q` $\rightarrow$ `h`, `u` $\rightarrow$ `o`, `v` $\rightarrow$ `r`, `l` $\rightarrow$ `a`
     - `w` $\rightarrow$ `p`, `b` $\rightarrow$ `u`, `p` $\rightarrow$ `e`, `g` $\rightarrow$ `g`
     - `n` $\rightarrow$ `i`, `o` $\rightarrow$ `n`, `x` $\rightarrow$ `d`, `a` $\rightarrow$ `m`, `c` $\rightarrow$ `y`
2. **Descifrado de la bandera**:
   - En la última línea del texto encontramos:
     ```text
     Fuv zqnt wvuhepa, zqp felg nt: lrlxpac{FV3DB3ORC_4774RM5_4V3_R001_0532L335}
     ```
   - Aplicando la sustitución obtenida y completando por contexto (*FREQUENCY ATTACKS ARE COOL*):
     - `lrlxpac` $\rightarrow$ `academy`
     - `FV3DB3ORC` $\rightarrow$ `FR3QU3NCY` (`F` $\rightarrow$ `F`, `V` $\rightarrow$ `R`, `D` $\rightarrow$ `Q`, `B` $\rightarrow$ `U`, `O` $\rightarrow$ `N`, `R` $\rightarrow$ `C`, `C` $\rightarrow$ `Y`)
     - `4774RM5` $\rightarrow$ `4774CK5` (`R` $\rightarrow$ `C`, `M` $\rightarrow$ `K`)
     - `4V3` $\rightarrow$ `4R3`
     - `R001` $\rightarrow$ `C001`
     - `0532L335` $\rightarrow$ `0532A335` (`L` $\rightarrow$ `A`)
Bandera obtenida: `academy{FR3QU3NCY_4774CK5_4R3_C001_0532A335}`
## Notas Adicionales
- **Script en Python para resolverlo**:
  `python`
  `known = {`
      `"r": "c",`
      `"z": "t",`
      `"f": "f",`
      `"t": "s",`
      `"q": "h",`
      `"u": "o",`
      `"v": "r",`
      `"l": "a",`
      `"w": "p",`
      `"b": "u",`
      `"p": "e",`
      `"g": "g",`
      `"c": "y",`
      `"a": "m",`
      `"n": "i",`
      `"o": "n",`
      `"x": "d",`
      `"j": "w",`
      `"e": "l",`
      `"m": "k",`
      `"h": "b",`
      `"s": "v",`
      `"d": "q",`
  `}`
  `with open("message.txt") as f:`
      `text = f.read()`
  `decrypted = []`
  `for ch in text:`
      `low = ch.lower()`
      `if low in known:`
          `sub = known[low]`
          `decrypted.append(sub.upper() if ch.isupper() else sub)`
      `else:`
          `decrypted.append(ch)`
  `print("".join(decrypted).splitlines()[-1])`
Herramientas de ataque por frecuencia online:
Plataformas como quipqiup.com
 o dcode.fr - Monoalphabetic Substitution
 utilizan modelos estadísticos basados en n-gramas del idioma inglés que resuelven este tipo de textos de manera completamente automática en menos de 1 segundo.
## Referencias
Análisis de frecuencias en criptoanálisis (Wikipedia)
quipqiup - Fast automated cryptogram solver
dcode.fr - Monoalphabetic Substitution Solver