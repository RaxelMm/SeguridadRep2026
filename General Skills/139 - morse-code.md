# Descripcion
Morse code is well known. Can you decrypt this? Download the file [here](https://challenge-files.cylabacademy.net/library/3728bfa4e8314fddd6b7e9f3fae9cb453b459a0bd4b3a29a9224701152f0cd89/morse_chal.wav).

Wrap your answer with academy{}, put underscores in place of pauses, and use all uppercase.

Hints

Audacity is a really good program to analyze morse code audio.
## Solución

El reto "morse-code" nos entrega un archivo de audio `morse_chal.wav` que reproduce una transmisión sonora en código Morse. La instrucción pide envolver el resultado con `academy{}`, sustituir las pausas entre palabras por guiones bajos (`_`) y mantener todas las letras en mayúsculas.

1. **Análisis de la señal de audio**:

   - Al cargar el archivo de audio en un programa de edición como **Audacity** (o analizar los picos de amplitud/envolvente con un script de Python), se observa una secuencia regular de tonos cortos (*dits* o puntos `.`) y largos (*dahs* o rayas `-`).

   - El mensaje transmitido hace referencia a la célebre frase bíblica ("*What hath God wrought*") enviada históricamente por Samuel Morse en 1844, pero escrita en *leetspeak* (sustituyendo letras por números):

2. **Decodificación del código Morse**:

   - `.--` `....` `....-` `--...` $\rightarrow$ **`WH47`** (*WHAT*)

   - `....` `....-` `--...` `....` $\rightarrow$ **`H47H`** (*HATH*)

   - `----.` `-----` `-..` $\rightarrow$ **`90D`** (*GOD*)

   - `.--` `..---` `-----` `..-` `----.` `....` `--...` $\rightarrow$ **`W20U9H7`** (*WROUGHT*)

3. **Formato**:

   - Uniendo las palabras separadas por pausas con `_` y envolviendo en `academy{}`:

     ```text

     academy{WH47_H47H_90D_W20U9H7}

     ```

Bandera obtenida: `academy{WH47_H47H_90D_W20U9H7}`

## Notas Adicionales

- **Resolución con Audacity**:

  - Al abrir el audio en Audacity y cambiar la vista de la pista a **Espectrograma** (*Spectrogram view*), los puntos y rayas se vuelven visibles como líneas cortas y largas en una frecuencia definida (~800 Hz).

- **Herramientas de decodificación automática online**:

  - Plataformas como [Morse Code World Audio Decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) permiten subir directamente el archivo `.wav` y transcriben los tonos a texto en segundos.

- **Resolución mediante script en Python**:

  python

  import wave, numpy as np

  # Leer envolvente y umbralizar

  with wave.open("morse_chal.wav", "rb") as w:

      audio = np.frombuffer(w.readframes(w.getnframes()), dtype=np.int16)

  # Segmentar por duración de señal activa e inactiva

  # Tonos <= 180 ms -> '.', > 180 ms -> '-'

  # Pausas entre letras ~ 300 ms, pausas entre palabras > 500 ms

## **Referencias**

- [Código Morse Internacional (Wikipedia)](https://es.wikipedia.org/wiki/C%C3%B3digo_morse)
- [Morse Code World - Adaptive Audio Decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html)
- [Audacity Audio Editor - Spectrogram View Guide](https://manual.audacityteam.org/man/spectrogram_view.html)