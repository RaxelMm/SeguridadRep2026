# Descripcion
We found this weird message being passed around on the servers, we think we have a working decryption scheme. Download the message [here](https://challenge-files.cylabacademy.net/library/f3895827512c6fab64095a69942e62ba9e367bb32d70ff69dc0e8fd9a826936a/message.txt).

Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.

Wrap your decrypted message in the academy flag format (i.e. `academy{decrypted_message}`)
## Solución

El reto "basic-mod1" nos proporciona un archivo de texto llamado `message.txt` con una serie de números enteros y nos especifica un algoritmo de descifrado basado en aritmética modular (módulo 37).

1. **Regla de mapeo**:

   - Cada número $n$ se reduce calculando el resto de su división entre 37:

     $$r = n \pmod{37}$$

   - El resultado $r$ (que estará en el rango de $0$ a $36$) se asigna al siguiente juego de caracteres:

     - `0 - 25`: Letras mayúsculas del abecedario (`A - Z`).

     - `26 - 35`: Dígitos decimales (`0 - 9`).

     - `36`: Guion bajo (`_`).

2. **Implementación y descifrado**:

   - Al procesar cada uno de los números del archivo `message.txt` con dicha tabla de sustitución, se obtiene la cadena en texto claro:

     ```text

     R0UND_N_R0UND_65371195

     ```

3. **Formateo**:

   - Siguiendo las instrucciones del reto, envolvemos el mensaje en el formato de bandera: `academy{R0UND_N_R0UND_65371195}`.

Bandera obtenida: `academy{R0UND_N_R0UND_65371195}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  `python`

  `import string`

  # `Conjunto de caracteres ordenado (longitud 37)`

  `charset = string.ascii_uppercase + string.digits + "_"`

  `with open("message.txt") as f:`

      `numbers = [int(x) for x in f.read().split()]`

  # `Aplicar modulo 37 y mapear al juego de caracteres`

  `decrypted = "".join(charset[n % 37] for n in numbers)`

  `print(f"academy{{{decrypted}}}")`

- **Aritmética Modular en Criptografía**: La operación módulo (n(modm)n \pmod mn(modm)) es uno de los pilares fundamentales de la criptografía moderna (cifrados de flujo, RSA, curvas elípticas, intercambio Diffie-Hellman), ya que permite trabajar dentro de un grupo algebraico finito asegurando que los números siempre pertenezcan a un conjunto acotado.

## **Referencias**

- [Aritmética modular (Wikipedia)](https://es.wikipedia.org/wiki/Aritm%C3%A9tica_modular)
- [Python modulo operator (%) reference](https://docs.python.org/3/reference/expressions.html#binary-arithmetic-operations)

