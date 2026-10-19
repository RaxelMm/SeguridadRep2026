# Descripcion
What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M∗∗e)(M∗∗e) is just barely larger than NN. Let's decrypt this: [values](https://challenge-files.cylabacademy.net/library/67cb1b8b1f3fd9565f722d725e2187148f945648e715823aaf1bdb6e4df7ade6/values)
## Solución

El reto "Mini RSA" nos entrega los parámetros de un cifrado RSA: el módulo $N$, el exponente público $e = 3$ y el texto cifrado $c$. 

En RSA, el cifrado se define como:

$$c \equiv M^e \pmod N \implies M^e = c + k \cdot N \quad (k \ge 0)$$

1. **Vulnerabilidad de exponente pequeño ($e = 3$)**:

   - Cuando el exponente público $e$ es muy pequeño y el mensaje $M$ no es lo suficientemente grande, $M^e$ puede no superar al módulo $N$ o superarlo por muy poco ($k$ muy pequeño).

   - En este caso, al probar $k = 0$, el valor $c$ es directamente un cubo perfecto en los enteros:

     $$M = \sqrt[3]{c}$$

2. **Cálculo de la raíz cúbica entera**:

   - Dado que los enteros en Python tienen precisión arbitraria, calculamos la raíz cúbica entera de $c$ (usando el método de Newton o búsqueda binaria) sin pérdida de precisión por conversión a punto flotante.

3. **Decodificación**:

   - Convertimos el entero $M$ a bytes, revelando un relleno de espacios en blanco seguido de la bandera:

     ```text

     "                                                                                                       academy{e_sh0u1d_b3_lArg3r_35f26e1a}\n"

     ```

Bandera obtenida: `academy{e_sh0u1d_b3_lArg3r_35f26e1a}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  python

  def integer_cube_root(n):

      x = 1 << ((n.bit_length() + 2) // 3)

      while True:

          y = (2 * x + n // (x * x)) // 3

          if y >= x:

              break

          x = y

      while (x + 1) ** 3 <= n:

          x += 1

      while x ** 3 > n:

          x -= 1

      return x

  with open("values") as f:

      lines = f.read().splitlines()

  c = int([l for l in lines if "ciphertext" in l][0].split(":")[1])

  m = integer_cube_root(c)

  # Convertir entero a bytes

  hex_str = hex(m)[2:]

  if len(hex_str) % 2 != 0:

      hex_str = "0" + hex_str

  print(bytes.fromhex(hex_str).decode("utf-8", errors="ignore"))

- **Con gmpy2**: Si se dispone de la biblioteca `gmpy2`, la operación es directa:
    
    python
    
    import gmpy2
    
    root, exact = gmpy2.iroot(c, 3)
    
    if exact:
    
        print(bytes.fromhex(hex(root)[2:]).decode())
    
- **Importancia del Padding**: Este ataque demuestra por qué nunca se debe utilizar RSA "de libro de texto" (_Textbook RSA_) sin esquemas de relleno criptográfico estandarizados como **OAEP** (Optimal Asymmetric Encryption Padding), los cuales garantizan que el mensaje ocupe todo el tamaño del módulo y evitan ataques directos de raíz eee-ésima.

## **Referencias**

- [Ataque de Exponente Pequeño en RSA (Wikipedia)](https://en.wikipedia.org/wiki/Coppersmith%27s_attack#Small_constant_exponent)
- [RFC 8017 - PKCS #1: RSA Cryptography Specifications (OAEP)](https://datatracker.ietf.org/doc/html/rfc8017)
- [Documentación gmpy2.iroot](https://gmpy2.readthedocs.io/en/latest/mpz.html#gmpy2.iroot)
