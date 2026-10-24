# Descripcion
We received an encrypted message. The modulus is built from primes large enough that factoring them isn’t an option, at least not today. See if you can make sense of the numbers and reveal the flag. Download the [message](https://challenge-files.cylabacademy.net/library/f688af3e0e10229b8e2533aeb1f2b70c566d6fbae5f7c0cce8374ad3c4d86651/message.txt).

## Solución

En el reto "Crack the Power", se nos proporciona un módulo RSA $n$ de 4096 bits, un exponente $e = 20$ y el texto cifrado $c$. La descripción aclara que factorizar $n$ no es factible.

1. **Vulnerabilidad de exponente pequeño sin reducción modular**:

   - En RSA, la operación de cifrado es:

     $$c = m^e \pmod n$$

   - Al comparar el tamaño en bits de los números, observamos que $n$ tiene **4096 bits**, mientras que el texto cifrado $c$ tiene **3813 bits**.

   - Como $c < n$, el valor de $m^{20}$ **nunca llegó a sobrepasar a $n$**, por lo que nunca ocurrió la operación módulo:

     $$c = m^{20}$$ directamente en el conjunto de los enteros ($\mathbb{Z}$).

2. **Cálculo de la raíz 20-ésima entera**:

   - No es necesario factorizar $n$ ni calcular la clave privada $d$; basta con calcular la raíz 20-ésima exacta de $c$:

     $$m = \sqrt[20]{c}$$

   - Mediante una búsqueda binaria o el método de Newton sobre enteros de precisión arbitraria en Python, encontramos la raíz exacta $m$.

3. **Decodificación**:

   - Al convertir el entero $m$ a bytes, obtenemos directamente la bandera en texto plano.

Bandera obtenida: `academy{t1ny_e_25f80100}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  python

  # Leer valores

  with open("message.txt") as f:

      lines = f.read().splitlines()

  for l in lines:

      if l.startswith("e ="):

          e = int(l.split("=")[1])

      elif l.startswith("c ="):

          c = int(l.split("=")[1])

  # Búsqueda binaria para la raíz e-ésima entera

  def nth_root(val, n):

      low = 0

      high = 1 << ((val.bit_length() + n - 1) // n + 1)

      while low <= high:

          mid = (low + high) // 2

          p = mid**n

          if p == val:

              return mid

          elif p < val:

              low = mid + 1

          else:

              high = mid - 1

      return None

  m = nth_root(c, e)

  # Convertir entero a bytes

  hex_str = hex(m)[2:]

  if len(hex_str) % 2:

      hex_str = "0" + hex_str

  print(bytes.fromhex(hex_str).decode())

- **Con gmpy2**:
    
    python
    
    import gmpy2
    
    m, exact = gmpy2.iroot(c, 20)
    
    if exact:
    
        print(bytes.fromhex(hex(m)[2:]).decode())
    
- **Falla fundamental de seguridad**: Este ataque es un caso extremo del ataque de Coppersmith / exponente pequeño sin relleno (_unpadded RSA_). Si el tamaño del mensaje en bits multiplicado por el exponente es menor que la longitud del módulo (∣m∣⋅e<∣n∣|m| \cdot e < |n|∣m∣⋅e<∣n∣), el cifrado deja de ser modular y se convierte en una simple exponenciación sobre enteros ordinarios.

## **Referencias**

- [Ataque de Exponente Pequeño en RSA (Wikipedia)](https://en.wikipedia.org/wiki/Coppersmith%27s_attack#Small_constant_exponent)
- [Twenty Years of Attacks on the RSA Cryptosystem - Dan Boneh](https://crypto.stanford.edu/~dabo/papers/RSA-survey.pdf)
- [gmpy2 Integer n-th Root Documentation](https://gmpy2.readthedocs.io/en/latest/mpz.html#gmpy2.iroot)