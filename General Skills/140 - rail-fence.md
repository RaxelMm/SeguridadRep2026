# Descripcion
A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it? Download the message [here](https://challenge-files.cylabacademy.net/library/d6cea3d41550d2d3e365dd3a7ea99fe9b44fe5fa437d1c921b5134a2070894a5/message.txt).

The decoded message names a phrase. Put that phrase, and nothing else, in the academy flag format: `academy{phrase}`.
## Solución

El reto "rail-fence" nos proporciona un archivo `message.txt` cifrado mediante el **Cifrado en Zigzag / Rail Fence Cipher** con una clave de **4 raíles** (*rails*).

1. **Funcionamiento del cifrado Rail Fence**:

   - El texto en claro se escribe en forma diagonal descendente y ascendente (patrón de zigzag) a través de $N$ niveles o rieles.

   - En este caso, con 4 raíles, el patrón de recorrido de índices de riel sigue el ciclo:

     $$0 \rightarrow 1 \rightarrow 2 \rightarrow 3 \rightarrow 2 \rightarrow 1 \rightarrow 0 \rightarrow \dots$$

   - Para descifrar, determinamos cuántos caracteres corresponden a cada riel según la longitud total del mensaje y reconstruimos la trayectoria original en zigzag.

2. **Descifrado con 4 rieles**:

   - Aplicando el algoritmo inverso sobre la cadena:

     `Ta _7N6D4Chlg:W3D_H3C31N__3E4ef sHR053F38N43DBC i33___NB`

   - Se obtiene el mensaje original:

     ```text

     The flag is: WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_43BBCEC4

     ```

3. **Formato**:

   - Siguiendo las instrucciones ("*Put that phrase, and nothing else, in the academy flag format*"), envolvemos únicamente la frase identificada:

     ```text

     academy{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_43BBCEC4}

     ```

Bandera obtenida: `academy{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_43BBCEC4}`

## Notas Adicionales

- **Script en Python para descifrado de Rail Fence**:

  `python`

  `def decrypt_rail_fence(ciphertext, num_rails):`

      `n = len(ciphertext)`

      `# 1. Determinar el orden de raíles por posición`

      `rail_indices = []`

      `rail, direction = 0, 1`

      `for _ in range(n):`

          `rail_indices.append(rail)`

          `rail += direction`

          `if rail == num_rails - 1:`

              `direction = -1`

          `elif rail == 0:`

              `direction = 1`

      `# 2. Asignar los caracteres a cada riel`

      `rails = {r: [] for r in range(num_rails)}`

      `idx = 0`

      `for r in range(num_rails):`

          `count = rail_indices.count(r)`

          `rails[r] = list(ciphertext[idx : idx + count])`

          `idx += count`

      `# 3. Leer siguiendo el zigzag`

      `plaintext = [rails[r].pop(0) for r in rail_indices]`

      `return "".join(plaintext)`

  `with open("message.txt") as f:`

      `c = f.read().strip()`

  `print(decrypt_rail_fence(c, 4))`

- **Resolución con CyberChef**:
    - En **CyberChef**, basta con añadir la operación **Rail Fence Cipher Decode** e indicar:
        - _Key / Number of Rails:_ `4`
        - _Offset:_ `0`
- **Tipo de cifrado**: A diferencia de los cifrados por sustitución (como César o Atbash), el Rail Fence es un **cifrado por transposición**, lo que significa que las letras originales no cambian, únicamente se reordena su posición en el mensaje.

## **Referencias**

- [Cifrado en Zigzag (Rail Fence Cipher) - Wikipedia](https://es.wikipedia.org/wiki/Cifrado_en_zigzag)
- [CyberChef - Rail Fence Decode](https://gchq.github.io/CyberChef/#recipe=Rail_Fence_Decode\(4,0\))
- [dcode.fr - Rail Fence Cipher Solver](https://www.dcode.fr/rail-fence-cipher)