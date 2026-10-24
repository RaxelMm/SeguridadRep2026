# Descripcion
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server? Access the server using `nc xebec.cylabacademy.net 36618`
## Solución

El reto "hashcrack" nos presenta un servicio accesible mediante `nc xebec.cylabacademy.net 36618` que requiere romper una secuencia de tres funciones hash comúnmente utilizadas y débiles (sin sal/salt y contraseñas comunes del diccionario):

1. **Ronda 1 (MD5)**:

   - **Hash recibido**: `482c811da5d5b4bc6d497ffa98491e38`

   - **Identificación**: 32 caracteres hexadecimales (128 bits) $\rightarrow$ algoritmo **MD5**.

   - **Cracking**: Consultando bases de datos de arcoíris (*rainbow tables* como CrackStation) o atacando con un diccionario básico como `rockyou.txt`, encontramos la contraseña:

     $$\text{MD5}(\text{"password123"}) = \text{482c811da5d5b4bc6d497ffa98491e38}$$

   - **Contraseña 1**: `password123`

2. **Ronda 2 (SHA-1)**:

   - **Hash recibido**: `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3`

   - **Identificación**: 40 caracteres hexadecimales (160 bits) $\rightarrow$ algoritmo **SHA-1**.

   - **Cracking**: Búsqueda por diccionario inverso:

     $$\text{SHA-1}(\text{"letmein"}) = \text{b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3}$$

   - **Contraseña 2**: `letmein`

3. **Ronda 3 (SHA-256)**:

   - **Hash recibido**: `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745`

   - **Identificación**: 64 caracteres hexadecimales (256 bits) $\rightarrow$ algoritmo **SHA-256**.

   - **Cracking**:

     $$\text{SHA-256}(\text{"qwerty098"}) = \text{916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745}$$

   - **Contraseña 3**: `qwerty098`

Al ingresar las 3 contraseñas en el servidor, este nos entrega el mensaje secreto con la bandera final.

Bandera obtenida: `academy{UseStr0nG_h@shEs_&PaSswDs!_a8894b1b}`

## Notas Adicionales

- **Script automático en Python**:

  python

  import socket, time

  s = socket.socket()

  s.connect(("xebec.cylabacademy.net", 36618))

  # 1. MD5

  s.recv(1024)

  s.sendall(b"password123\n")

  time.sleep(0.5)

  # 2. SHA-1

  s.recv(1024)

  s.sendall(b"letmein\n")

  time.sleep(0.5)

  # 3. SHA-256

  s.recv(1024)

  s.sendall(b"qwerty098\n")

  time.sleep(0.5)

  # Resultado

  print(s.recv(4096).decode())

  s.close()

- **Identificación de algoritmos hash por longitud**:
    - `32 caracteres hex (128 bits)`: Generalmente **MD5** o NTLM.
    - `40 caracteres hex (160 bits)`: Generalmente **SHA-1**.
    - `64 caracteres hex (256 bits)`: Generalmente **SHA-256**.
- **Herramientas para descifrado de hashes**:
    - **Online**: [CrackStation](https://crackstation.net/) contiene bases de datos precomputadas de miles de millones de hashes comunes.
    - **Offline**: Herramientas como **Hashcat** o **John the Ripper** combinadas con la lista de palabras `rockyou.txt` permiten romper estos hashes en fracciones de segundo.

## **Referencias**

- [CrackStation - Free Hash Lookup Service](https://crackstation.net/)
- [Hashcat - Advanced Password Recovery](https://hashcat.net/hashcat/)
- [NIST Guidelines on Password Hashing and Salting](https://pages.nist.gov/800-63-3/sp800-63b.html)