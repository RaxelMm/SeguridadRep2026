# Descripcion
Decode this [message](https://challenge-files.cylabacademy.net/library/d825fde6581b1311eafdd403da1cc96f1f98fe3fe84cd71d850310ebb3908088/message.wav) from the moon.

## Solucion
1. Descargar `message.wav`.
2. Identificar que es SSTV (imágenes transmitidas como audio).
3. Decodificar con `sstv -d message.wav -o moonwalk_result.png`.
4. Abrir la imagen generada y leer la flag.
## Notas Adicionales
- Pista 1: Las imágenes del Apolo se transmitían vía SSTV.
- Pista 2: Mascota CMU = Scotty → modo **Scottie 1**.
- Alternativa: QSSTV con cable virtual (`pactl load-module module-null-sink`).
- Flag: `picoCTF{beep_boop_im_in_space}`
## Referencias
- picoCTF 2019 - m00nwalk (Forensics, Medium)
- Herramienta: https://github.com/colaclanth/sstv
- SSTV Wikipedia
