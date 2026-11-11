# Descripcion
The name of the game is [speed](https://www.youtube.com/watch?v=8piqd2BWeGI). Are you quick enough to solve this problem and keep it above 50 mph? [need-for-speed](https://challenge-files.cylabacademy.net/library/1f19c0ef7346746915a41e424dc8399c20e09955cc88570026df8750f77905bf/need-for-speed).
## **Solución**

El binario establece un `alarm(SIGALRM)` que lo mata si tarda demasiado — de ahí el nombre "Need for Speed". El flujo es:

1. `calculate_key()` ejecuta un loop deliberadamente lento (doble bucle con ~570M iteraciones totales) para gastar tiempo y hacer que el `alarm` lo mate antes de imprimir el flag.
2. `get_key()` llama a `calculate_key()` y guarda el resultado (`0xddf3851e`) en una variable global.
3. `decrypt_flag(key)` descifra los 55 bytes del flag en `.data` usando XOR con los bytes del key (alternando byte 0 y byte 1 del key en little-endian). Cada 3 bytes (`i%3==2`), el key se incrementa en 1.
4. `print_flag()` imprime el resultado.

Se extrajo estáticamente el key (`0xddf3851e`) y los datos cifrados en `.data:0x4020`, y se aplicó la misma lógica de XOR en Python para obtener el flag.

**Flag:** `academy{Good job keeping bus #251feedf speeding along!}`

## **Notas Adicionales**

- La "velocidad" del desafío es una ilusión: el verdadero obstáculo es el `alarm()` que mata el proceso antes de que el bucle lento de `calculate_key` termine. Saltarlo con GDB (`disable alarm`) o resolver estáticamente son las soluciones.
- El key final es **siempre** `0xddf3851e` porque el bucle interno siempre termina en ese valor exacto.
- La cifra usa XOR alternado de 2 bytes del key, con incremento cada 3 caracteres — una variante simple de stream cipher.
- El número `#251feedf` en el flag es el key mismo (`0xddf3851e` ≠ `0x251feedf`... de hecho es parte del mensaje del flag, no el key).

## **Referencias**

- [x86-64 integer division magic numbers](https://ridiculousfish.com/files/clang_divconstant.pdf)
- [SIGALRM / alarm()](https://man7.org/linux/man-pages/man2/alarm.2.html)
- [GDB: disable signal handling](https://sourceware.org/gdb/current/onlinedocs/gdb/Signals.html)