# Descripcion
Can you decrypt this message? Decrypt this [message](https://challenge-files.cylabacademy.net/library/1415ede8e9f58b36fddf7b520d73c151a53ac100c476ca97c7a19f9b901100d3/cipher.txt) using this key "CYLAB".
## Solución

El reto "Vigenere" nos proporciona un archivo llamado `cipher.txt` y nos indica la clave para descifrarlo: **`CYLAB`**.

1. **El Cifrado Vigenère**:

   - Es un cifrado por sustitución polialfabética que utiliza una palabra clave para desplazar cíclicamente cada letra del mensaje según el índice alfabético de la letra de la clave ($A = 0, B = 1, \dots, Z = 25$):

     $$P_i = (C_i - K_{i \pmod L}) \pmod{26}$$

   - Los caracteres no alfabéticos (como números, guiones bajos `{`, `_`, `}`, `0-9`) no se modifican y no avanzan la posición de la clave.

2. **Descifrado**:

   - Texto cifrado: `caldfow{O0NU_WQ3_G1G3O3T3_A1AH3S_a0393cd7}`

   - Clave: `CYLAB`

   - Aplicando el desplazamiento inverso letra por letra:

     - `caldfow` $\rightarrow$ `academy`

     - `O0NU` $\rightarrow$ `D0NT`

     - `WQ3` $\rightarrow$ `US3`

     - `G1G3O3T3` $\rightarrow$ `V1G3N3R3`

     - `A1AH3S` $\rightarrow$ `C1PH3R`

     - `a0393cd7` $\rightarrow$ `y0393es7`

   - El mensaje descifrado dice: *"DONT USE VIGENERE CIPHER"* ("No uses el cifrado Vigenère").

Bandera obtenida: `academy{D0NT_US3_V1G3N3R3_C1PH3R_y0393es7}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  `python`

  `def decrypt_vigenere(ciphertext, key):`

      `res = []`

      `key = key.upper()`

      `k_len = len(key)`

      `k_idx = 0`

      `for ch in ciphertext:`

          `if ch.isalpha():`

              `base = ord("A") if ch.isupper() else ord("a")`

              `shift = ord(key[k_idx % k_len]) - ord("A")`

              `res.append(chr((ord(ch) - base - shift) % 26 + base))`

              `k_idx += 1`

          `else:`

              `res.append(ch)`

      `return "".join(res)`

  `with open("cipher.txt") as f:`

      `ct = f.read().strip()`

  `print(decrypt_vigenere(ct, "CYLAB"))`

- **Resolución con CyberChef**:
    - En **CyberChef**, basta con añadir la operación **Vigenère Decode**, establecer la clave en `CYLAB` y mantener el alfabeto estándar.
- **Seguridad histórica del cifrado**: Durante siglos el cifrado Vigenère fue conocido como _le chiffre indéchiffrable_ ("el cifrado indescifrable"). Sin embargo, en el siglo XIX Friedrich Kasiski demostró que puede romperse fácilmente encontrando repeticiones de patrones para determinar la longitud de la clave y aplicando análisis de frecuencias independiente a cada subalfabeto.

## **Referencias**

- [Cifrado de Vigenère (Wikipedia)](https://es.wikipedia.org/wiki/Cifrado_de_Vigen%C3%A8re)
- [CyberChef - Vigenère Decode](https://gchq.github.io/CyberChef/#recipe=Vigen%C3%A8re_Decode\('CYLAB'\))
- [Examen de Kasiski - Criptoanálisis de Vigenère](https://es.wikipedia.org/wiki/M%C3%A9todo_Kasiski)

