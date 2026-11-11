# Descripcion
We have recovered a [binary](https://challenge-files.cylabacademy.net/library/4de47cc73b1c6e4976e058249b7181cfe15c64e28b5a4a0a54edefdf6608f118/rev) and a [text file](https://challenge-files.cylabacademy.net/library/4de47cc73b1c6e4976e058249b7181cfe15c64e28b5a4a0a54edefdf6608f118/rev_this). Can you reverse the flag.
## **Solución**

El binario `rev` lee `flag.txt`, copia los primeros 8 caracteres (`academy{`) sin cambios, luego aplica a los siguientes bytes una transformación basada en la **paridad del índice**:

- Índice **par** → `c + 5`
- Índice **impar** → `c - 2`

Finalmente copia el `}` final sin cambios y escribe el resultado en `rev_this`.

Para recuperar el flag, se invierte: par → `c - 5`, impar → `c + 2`.

**Flag:** `academy{r3v3rs397436647}`

## **Notas Adicionales**

- El binario es x86-64 ELF (Debian/Linux). Se analizó estáticamente parseando la sección `.text` con Python.
- La transformación opera solo sobre el cuerpo del flag (bytes 8–22), no sobre el prefijo ni el `}`.
- Leer el `fread` con tamaño 24 (0x18) fija el largo esperado del flag a exactamente 24 bytes.
- La función `main` controla dos loops: `for i in 0..7` (copia directa) y `for i in 8..22` (cifrado).

## **Referencias**

- [x86-64 calling convention](https://refspecs.linuxbase.org/elf/x86_64-abi-0.99.pdf)
- [Objdump usage](https://man7.org/linux/man-pages/man1/objdump.1.html)
- [ELF format reference](https://refspecs.linuxbase.org/elf/elf.pdf)
