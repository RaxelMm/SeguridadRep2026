# Descripcion
In RSA, a small ee value can be problematic, but what about NN? Can you decrypt this? [values](https://challenge-files.cylabacademy.net/library/c800df9c0f52301295a618b2bff7362cf61388e5a04f135b01c9693fdf7a09e8/values)

## Solución

El reto nos entrega tres parámetros RSA: el módulo $N$ (de solo **270 bits**), el exponente público $e = 65537$ y el texto cifrado $c$.

La vulnerabilidad aquí es un **módulo $N$ demasiado pequeño**, ya que la seguridad de RSA depende de que la factorización de $N = p \cdot q$ sea computacionalmente inviable.

1. **Factorización de $N$**:

   - Con solo 270 bits, $N$ es factorizable en segundos con herramientas modernas.

   - Consultando la base de datos [FactorDB](https://factordb.com), obtenemos los factores primos directamente:

     - $p = 2074606527507983503944226222695401999839$

     - $q = 659880377875535146491994798968813949893149$

   - Se verifica: $p \times q = N$.

2. **Cálculo de la clave privada $d$**:

   - Calculamos $\phi(N) = (p - 1)(q - 1)$.

   - La clave privada se obtiene como el inverso modular: $d = e^{-1} \pmod{\phi(N)}$.

3. **Descifrado**:

   - El mensaje original se recupera con: $M = c^d \pmod N$.

   - Convirtiendo el entero $M$ a bytes, los caracteres salen en orden inverso (consecuencia de cómo se almacenó el mensaje), así que se revierten para obtener la bandera legible.

Bandera obtenida: `academy{sma11_N_n0_g0od_a3ac7152}`

## Notas Adicionales

- **Script Python completo**:

  python

  p = 2074606527507983503944226222695401999839

  q = 659880377875535146491994798968813949893149

  e = 65537

  c = 717608817902276639011922897702552744324264244069272484013719744328086856277690292

  phi = (p - 1) * (q - 1)

  d = pow(e, -1, phi)

  m = pow(c, d, p * q)

  hex_str = hex(m)[2:]

  if len(hex_str) % 2:

      hex_str = "0" + hex_str

  flag = bytes.fromhex(hex_str)[::-1].decode()

  print(flag)

- **Recomendación RSA en la práctica**: Los estándares actuales (NIST) recomiendan claves RSA de **mínimo 2048 bits**, siendo 4096 bits para uso a largo plazo. Con 270 bits, un atacante puede factorizar NNN en cuestión de segundos usando herramientas como `msieve`, `yafu` o simplemente consultando FactorDB.
- **Herramienta de factorización**: [FactorDB.com](https://factordb.com) mantiene una base de datos de números ya factorizados. Si NNN es suficientemente pequeño, probablemente ya esté indexado.

## **Referencias**

- [FactorDB - Base de datos de factorizaciones](https://factordb.com)
- [RSA Key Sizes - NIST Recommendations](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final)
- [RSA Cryptosystem (Wikipedia)](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\))