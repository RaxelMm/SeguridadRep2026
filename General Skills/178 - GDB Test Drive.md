# Descripcion
Can you get the flag? Download this [binary](https://challenge-files.cylabacademy.net/library/394cd9dfa2b4d40f74f2ad999c1ea208ed4daf3382f56b3372ca33b69756a65d/gdbme).

Here's the test drive instructions:

- `$ chmod +x gdbme`
- `$ gdb gdbme`
- `(gdb) layout asm`
- `(gdb) break *(main+99)`
- `(gdb) run`
- `(gdb) jump *(main+104)`
## **Solución**

El binario `gdbme` almacena el flag ofuscado con **ROT47** directamente en el stack de `main`. La función `rotate_encrypt` aplica ROT47 al string cifrado y el resultado se imprime con `fputs`. El truco del desafío es que `sleep(100000)` se llama justo antes — en GDB se salta esa instrucción con `jump *(main+104)`.

Se extrajo el string cifrado del binario (`24256>JL5b3F88bC05C`Gb077dbah7`N`) y se aplicó ROT47 estáticamente para obtener el flag sin necesitar GDB ni Linux.

**Flag:** `academy{d3bugg3r_dr1v3_ff5329f1}`

## **Notas Adicionales**

- ROT47 opera sobre los 94 caracteres imprimibles ASCII (0x21–0x7e), sumando 47 y haciendo wrapping. Es **auto-inverso** (aplicarlo dos veces da el texto original).
- El binario es un ELF x86-64 de Linux — en Windows se analizó estáticamente parseando el ELF manualmente con Python (`struct`).
- `sleep()` recibe `0x186a0` = 100,000 segundos (~27.7 horas). El GDB jump omite esa llamada.
- La función `rotate_encrypt` ignora su primer argumento (edi=0); solo procesa el string recibido por rsi.

## **Referencias**

- [ROT47 cipher](https://en.wikipedia.org/wiki/ROT13#Variants)
- [x86-64 ELF structure](https://refspecs.linuxbase.org/elf/elf.pdf)
- [GDB jump command](https://sourceware.org/gdb/current/onlinedocs/gdb/Jumping.html).
