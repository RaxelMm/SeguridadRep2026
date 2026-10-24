# Descripcion
This service provides you an encrypted flag. Can you decrypt it with just N & e? Connect to the program with netcat:

`$ nc chatelaine.cylabacademy.net 34498`

The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/8d8b38c88a9606bca290997e6dc1bd9205ebc794cf16c913a56b487dbf220849/encrypt.py).
## Solución

El reto "EVEN RSA CAN BE BROKEN???" nos conecta a un servicio por `nc` que genera una clave RSA y nos devuelve el módulo $N$, el exponente $e = 65537$ y el texto cifrado (*cyphertext*).

1. **Análisis del juego de palabras y del número $N$**:

   - El título del reto hace un juego de palabras literal con la palabra en inglés **EVEN** (que significa "par" y a su vez "incluso").

   - Al observar el último dígito del módulo $N$ recibido desde el servidor (terminado en 2, 4, 8, etc.), descubrimos que **$N$ es un número par**.

2. **Factorización trivial ($p = 2$)**:

   - En RSA, $N = p \cdot q$, donde $p$ y $q$ son números primos. Como el número 2 es el único número primo par, uno de los factores primos de la clave es forzosamente:

     $$p = 2$$

   - Por tanto, el segundo primo se obtiene simplemente dividiendo $N$ entre 2:

     $$q = \frac{N}{2}$$

3. **Cálculo de la clave privada $d$ y descifrado**:

   - Calculamos la función de Euler:

     $$\phi(N) = (p - 1)(q - 1) = (2 - 1)(q - 1) = q - 1 = \frac{N}{2} - 1$$

   - Obtenemos el exponente privado $d$:

     $$d \equiv e^{-1} \pmod{\phi(N)}$$

   - Desciframos el mensaje:

     $$m = c^d \pmod N$$

   - Convertimos el entero $m$ a texto plano para obtener la bandera.

Bandera obtenida: `academy{tw0_1$_pr!m3cfb893a9}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  python

  import socket

  # Conectar al servicio y recibir N, e, c

  def solve():

      s = socket.socket()

      s.connect(("chatelaine.cylabacademy.net", 34498))

      data = s.recv(4096).decode()

      s.close()

      lines = data.strip().split("\n")

      N = int([l for l in lines if l.startswith("N:")][0].split(":")[1])

      e = int([l for l in lines if l.startswith("e:")][0].split(":")[1])

      c = int([l for l in lines if "cyphertext:" in l][0].split(":")[1])

      # Como N es par, p = 2

      p = 2

      q = N // 2

      phi = (p - 1) * (q - 1)

      d = pow(e, -1, phi)

      m = pow(c, d, N)

      hex_str = hex(m)[2:]

      if len(hex_str) % 2:

          hex_str = "0" + hex_str

      print("Bandera:", bytes.fromhex(hex_str).decode())

  solve()

- **Por qué ocurre esta debilidad**: En la generación segura de claves RSA, la función generadora de números primos debe descartar explícitamente el primo 222 y generar únicamente primos impares de gran tamaño (mínimo 1024 o 2048 bits cada uno). Si el generador incluye el rango desde 2, existe la posibilidad de que seleccione p=2p = 2p=2, haciendo la factorización trivial e instantánea.

## **Referencias**

- [Definición de Números Primos y Paridad (Wikipedia)](https://es.wikipedia.org/wiki/N%C3%BAmero_primo)
- [RSA Key Generation Specifications - RFC 8017](https://datatracker.ietf.org/doc/html/rfc8017#section-3.1)
- [Ataques a RSA con primos débiles o predecibles](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\)#Attacks_against_plain_RSA)