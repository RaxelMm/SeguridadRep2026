# Descripcion
We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it? Download the leak [here](https://challenge-files.cylabacademy.net/library/7f760cee144ac7237469fd6bfab7c748d6f1d101ca47c101187ca7d8f5c721f0/leak.tar).

The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.
## Solución

El reto "credstuff" nos proporciona un archivo comprimido `leak.tar` que contiene una filtración de credenciales con dos archivos de texto: `usernames.txt` y `passwords.txt`. Cada línea en `usernames.txt` se corresponde de forma unívoca con la misma línea en `passwords.txt`.

1. **Localizar al usuario objetivo**:

   - Buscamos el usuario `cultiris` dentro de `usernames.txt`. Se encuentra en la **línea 378**.

2. **Obtener la contraseña asociada**:

   - Consultamos la línea 378 de `passwords.txt`, donde encontramos la siguiente cadena cifrada:

     ```text

     npnqrzl{P7e1S_54I35_71Z3}

     ```

3. **Descifrado con ROT13**:

   - Al observar el formato `npnqrzl{...}`, reconocemos el patrón típico del cifrado César con desplazamiento de 13 posiciones (**ROT13**), donde `npnqrzl` corresponde a `academy`.

   - Aplicando ROT13 a toda la cadena:

     - `npnqrzl` $\rightarrow$ `academy`

     - `P7e1S` $\rightarrow$ `C7r1F` (*CtrlF*)

     - `54I35` $\rightarrow$ `54V35` (*SAVES*)

     - `71Z3` $\rightarrow$ `71M3` (*TIME*)

Bandera obtenida: `academy{C7r1F_54V35_71M3}`

## Notas Adicionales

- **Resolución rápida en Bash / Linux**:

  bash

  # 1. Descomprimir el tar

  tar -xf leak.tar

  # 2. Encontrar el número de línea de 'cultiris'

  LINE=$(grep -n "^cultiris$" leak/usernames.txt | cut -d: -f1)

  # 3. Extraer la contraseña correspondiente y decodificar con ROT13 (tr)

  sed -n "${LINE}p" leak/passwords.txt | tr "A-Za-z" "N-ZA-Mn-za-m"

- **Resolución con Python**:
    
    python
    
    import codecs
    
    with open("leak/usernames.txt") as u, open("leak/passwords.txt") as p:
    
        users = [x.strip() for x in u]
    
        passwords = [x.strip() for x in p]
    
    idx = users.index("cultiris")
    
    pwd = passwords[idx]
    
    flag = codecs.decode(pwd, "rot_13")
    
    print("Bandera:", flag)
    
- **El chiste del reto**: El texto en leetspeak dentro de la bandera dice `CtrlF_SAVES_TIME` ("Ctrl+F ahorra tiempo"), haciendo alusión humorística a que no era necesario revisar las 505 líneas manualmente, sino simplemente usar el comando de búsqueda de cualquier editor de texto o terminal.

## **Referencias**

- [ROT13 (Wikipedia)](https://es.wikipedia.org/wiki/ROT13)
- [GNU grep y sed manual](https://www.gnu.org/software/grep/manual/grep.html)
- [CyberChef - ROT13 Recipe](https://gchq.github.io/CyberChef/#recipe=ROT13\(true,true,false,13\))
