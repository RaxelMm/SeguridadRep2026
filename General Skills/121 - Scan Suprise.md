# Descripcion
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?

You can download the challenge files here:

- [challenge.zip](https://challenge-files.cylabacademy.net/library/e48eb57d2e3cbfa7fc0b3f0023b5de68ffbea6ed090caca4ceeaf403fdc00f9b/challenge.zip)
## Solución
Para resolver el reto "Scan Surprise", se nos entrega un archivo comprimido llamado `challenge.zip`.

1. Descomprimimos el archivo `challenge.zip`, el cual contiene la ruta `home/ctf-player/drop-in/flag.png`.
2. Al abrir o inspeccionar la imagen resultante, descubrimos que se trata de un código QR.
3. Escaneamos/decodificamos el código QR (utilizando la cámara de un teléfono, herramientas de terminal como `zbarimg` o un detector en Python mediante OpenCV).
4. El contenido almacenado en el código QR revela la bandera en texto claro.

Bandera obtenida: `academy{p33k_@_b00_a2658a69}`

## Notas Adicionales
- **Resolución desde el móvil**: Simplemente abriendo la imagen en pantalla y apuntando con la cámara de cualquier teléfono moderno (iOS o Android) se decodifica automáticamente el texto.
- **Resolución en Linux / CLI**:
  - Puedes usar `zbar-tools` ejecutando:
    ```bash
    zbarimg flag.png
    ```
- **Resolución con Python**:
  - Se puede decodificar programáticamente usando `opencv-python`:
    ```python
    import cv2
    img = cv2.imread("flag.png")
    detector = cv2.QRCodeDetector()
    data, _, _ = detector.detectAndDecode(img)
    print(data)
    ```

## Referencias
- [ZBar Bar Code Reader / zbarimg documentation](http://zbar.sourceforge.net/)
- [OpenCV QRCodeDetector Documentation](https://docs.opencv.org/4.x/de/dc3/classcv_1_1QRCodeDetector.html)
- [QR Code Specification Overview](https://es.wikipedia.org/wiki/C%C3%B3digo_QR)
