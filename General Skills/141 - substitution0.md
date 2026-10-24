# Descripcion
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://challenge-files.cylabacademy.net/library/0a2e91276318c0f6d400f5096fdaf87fcf57f37ebabf90004552502979a581c8/message.txt).
## Solución

El reto "substitution0" nos proporciona un archivo `message.txt` cifrado mediante un **cifrado por sustitución monoalfabética**. Como indica la descripción, la clave completa de sustitución se incluye al inicio del documento.

1. **Identificación de la clave**:

   - La primera línea del archivo contiene la permutación de 26 letras:

     ```text

     HRZUEVABDLIOJYTGNXCMWPKSQF

     ```

   - Cada letra del alfabeto estándar (`A-Z`) fue reemplazada por la letra que ocupa esa misma posición en la clave:

     - Posición 0: `H` $\rightarrow$ `A`

     - Posición 1: `R` $\rightarrow$ `B`

     - Posición 2: `Z` $\rightarrow$ `C`

     - ... y así sucesivamente.

2. **Descifrado**:

   - Creamos una tabla de sustitución inversa mapeando `HRZUEVABDLIOJYTGNXCMWPKSQF` hacia `ABCDEFGHIJKLMNOPQRSTUVWXYZ` (tanto para mayúsculas como minúsculas).

   - Al descifrar el texto (un fragmento clásico del cuento *El escarabajo de oro* de Edgar Allan Poe), la última línea revela la bandera:

     ```text

     The flag is: academy{5UB5717U710N_3V0LU710N_4FBD1EB7}

     ```

Bandera obtenida: `academy{5UB5717U710N_3V0LU710N_4FBD1EB7}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  `python`

  `import string`

  `key = "HRZUEVABDLIOJYTGNXCMWPKSQF"`

  `alphabet = string.ascii_uppercase`

  `with open("message.txt") as f:`

      `text = f.read()`

  # `Mapeo tanto para mayúsculas como minúsculas`

  `trans = str.maketrans(key + key.lower(), alphabet + alphabet.lower())`

  `decrypted = text.translate(trans)`

  `print(decrypted.splitlines()[-1])`

- **Resolución sin clave (Análisis de Frecuencias)**:
    - Si no tuviéramos la clave al principio del archivo, se resolvería mediante análisis de frecuencia de letras en inglés (la `e`, `t`, `a` son las más comunes, `the` como trígrafo frecuente) o subiendo el texto a herramientas de resolución automática como **quipqiup** o **dcode.fr**.
- **Contexto histórico**: El texto utilizado es del relato _The Gold-Bug_ (El escarabajo de oro) de Edgar Allan Poe, una de las obras literarias más famosas que popularizó la criptografía y el análisis de frecuencias entre el público general.

## **Referencias**

- [Cifrado por sustitución monoalfabética (Wikipedia)](https://es.wikipedia.org/wiki/Cifrado_por_sustituci%C3%B3n)
- [quipqiup - Automated Substitution Cipher Solver](https://www.quipqiup.com/)
- [The Gold-Bug de Edgar Allan Poe (Análisis criptográfico)](https://en.wikipedia.org/wiki/The_Gold-Bug)

