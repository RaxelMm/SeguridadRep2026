# Descripcion
 What do the [flags](https://challenge-files.cylabacademy.net/library/187296d0c352a8451662153842fc9794b9f247a1ac949978113ddfcb9a1bb76f/flag.png) mean?
## Solución
El reto "flags" nos presenta una imagen `flag.png` compuesta por una hilera de banderas náuticas y corchetes `{ }`. La pista nos indica que el formato de la bandera es `PICOCTF{}`.

1. **Identificación del alfabeto**:
   - Las figuras corresponden al **Código Internacional de Señales marítimas (ICS)** y a los gallardetes numéricos utilizados por la OTAN / navegación internacional para comunicarse visualmente entre embarcaciones.

2. **Decodificación de la cabecera (antes de las llaves)**:
   - Azul con cuadrado blanco central $\rightarrow$ **P** (*Papa*)
   - Amarillo con círculo negro $\rightarrow$ **I** (*India*)
   - Rayas horizontales azul-blanco-rojo-blanco-azul $\rightarrow$ **C** (*Charlie*)
   - Diagonal rojo y amarillo $\rightarrow$ **O** (*Oscar*)
   - Rayas horizontales azul-blanco-rojo-blanco-azul $\rightarrow$ **C** (*Charlie*)
   - Franjas verticales rojo-blanco-azul $\rightarrow$ **T** (*Tango*)
   - Blanco con rombo rojo $\rightarrow$ **F** (*Foxtrot*)
   - Forma el prefijo: **`PICOCTF`**

3. **Decodificación del interior `{ ... }`**:
   - Blanco con rombo rojo $\rightarrow$ **F**
   - Franjas horizontales roja-amarilla-roja (Gallardete OTAN) $\rightarrow$ **1**
   - Gallardete bífido blanco y azul $\rightarrow$ **A** (*Alfa*)
   - Rayas verticales amarillas y azules $\rightarrow$ **G** (*Golf*)
   - Cruz de San Andrés amarilla sobre fondo azul (Gallardete OTAN) $\rightarrow$ **5**
   - Gallardete bífido blanco y azul $\rightarrow$ **A** (*Alfa*)
   - Tablero de ajedrez azul y blanco $\rightarrow$ **N** (*November*)
   - Franjas horizontales azul-amarillo-azul $\rightarrow$ **D** (*Delta*)
   - Cruz de San Andrés amarilla sobre fondo azul $\rightarrow$ **5**
   - Franjas verticales rojo-blanco-azul $\rightarrow$ **T** (*Tango*)
   - Cuartelado rojo y blanco $\rightarrow$ **U** (*Uniform*)
   - Blanco con rombo rojo $\rightarrow$ **F** (*Foxtrot*)
   - Blanco con rombo rojo $\rightarrow$ **F** (*Foxtrot*)
   - Texto resultante: `F1AG5AND5TUFF` (*"FLAGS AND STUFF"* en l33t).

Bandera obtenida: `PICOCTF{F1AG5AND5TUFF}`

## Notas Adicionales
- **Diferencia entre banderas de letras y números**: Las letras estándar provienen del Código Internacional de Señales (ICS), mientras que los dígitos numéricos en este reto usan el estándar de señalización de la OTAN (*NATO numeral flags*), lo que permite alternar letras y números en leetspeak (`1` en lugar de `L`, `5` en lugar de `S`).
- **Herramientas de decodificación rápida**: En plataformas como **dcode.fr** existe una herramienta específica llamada *International Maritime Signal Flags* que permite hacer clic en las banderas vistas en la imagen para traducirlas instantáneamente a texto.

## Referencias
- [International Code of Signals - Maritime Flags (Wikipedia)](https://en.wikipedia.org/wiki/International_maritime_signal_flags)
- [dcode.fr - Maritime Signal Flags Decoder](https://www.dcode.fr/maritime-signals-code)
- [NATO Naval Flags and Pennants](https://en.wikipedia.org/wiki/NATO_phonetic_alphabet#Signal_flags)
