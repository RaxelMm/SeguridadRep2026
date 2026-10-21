# Descripcion
How about some hide and seek heh? Look at this image [here](https://challenge-files.cylabacademy.net/library/4430e164c62a6474394efb666c3b2c24511a0823a3408e5e7a19a37940f0e592/atbash.jpg).
## Solución

El reto "HideToSee" nos proporciona una imagen llamada `atbash.jpg` que muestra el disco de cifrado del método Atbash. El nombre del reto (*HideToSee*) y la pista (*"Download the image and try to extract it"*) hacen alusión directa al uso de la herramienta de esteganografía **Steghide**.

1. **Extracción con Steghide**:

   - Extraemos los datos ocultos dentro de la imagen `atbash.jpg` utilizando una contraseña vacía (*passphrase* en blanco):

     ```bash

     steghide extract -sf atbash.jpg -p ""

     ```

   - Esto extrae un archivo de texto llamado `encrypted.txt` con el siguiente contenido cifrado:

     ```text

     zxzwvnb{zgyzhs_xizxp_6167yw8v}

     ```

2. **Descifrado con Cifrado Atbash**:

   - Tal como sugiere la imagen del reto, el texto está cifrado mediante el **Cifrado Atbash** (un cifrado por sustitución monoalfabética que invierte el abecedario: $A \leftrightarrow Z$, $B \leftrightarrow Y$, $C \leftrightarrow X$, etc.).

   - Al aplicar la transformación inversa a las letras de `zxzwvnb{zgyzhs_xizxp_6167yw8v}`:

     - `zxzwvnb` $\rightarrow$ `academy`

     - `zgyzhs` $\rightarrow$ `atbash`

     - `xizxp` $\rightarrow$ `crack`

     - `6167yw8v` $\rightarrow$ `6167bd8e`

Bandera obtenida: `academy{atbash_crack_6167bd8e}`

## Notas Adicionales

- **Script en Python para resolverlo**:

  `python`

  `import subprocess`

  # `1. Extraer el archivo con steghide (passphrase vacía)`

  `def extract_and_solve():`

      `subprocess.run(["steghide", "extract", "-sf", "atbash.jpg", "-p", ""])`

      `with open("encrypted.txt") as f:`

          `ciphertext = f.read().strip()`

      `# 2. Descifrar con Atbash`

      `def atbash(text):`

          `res = []`

          `for c in text:`

              `if "a" <= c <= "z":`

                  `res.append(chr(ord("z") - (ord(c) - ord("a"))))`

              `elif "A" <= c <= "Z":`

                  `res.append(chr(ord("Z") - (ord(c) - ord("A"))))`

              `else:`

                  `res.append(c)`

          `return "".join(res)`

      `print("Bandera:", atbash(ciphertext))`

  `extract_and_solve()`

- `**Cifrado Atbash**: Es uno de los cifrados clásicos más antiguos conocidos (de origen hebreo bíblico). Dado que su función de cifrado es involutiva (E(E(x))=xE(E(x)) = xE(E(x))=x), el mismo algoritmo se utiliza tanto para cifrar como para descifrar.`
- `**Herramientas alternativas**: Para descifrar el texto Atbash rápidamente sin programar, se puede recurrir a herramientas web como **CyberChef** (operación _Atbash Cipher_) o **dcode.fr**.`

## **Referencias**

- [Steghide - Software de esteganografía](https://steghide.sourceforge.net/)
- [Cifrado Atbash (Wikipedia)](https://es.wikipedia.org/wiki/Atbash)
- [CyberChef - Atbash Cipher](https://gchq.github.io/CyberChef/#recipe=Atbash_Cipher\(\))

