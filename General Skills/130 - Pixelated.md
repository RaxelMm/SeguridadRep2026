# Descripcion
I have these 2 images, can you make a flag out of them?
## Solución

El reto "Pixelated" nos proporciona dos imágenes aparentemente compuestas por ruido aleatorio: `scrambled1.png` y `scrambled2.png`. Las pistas hacen referencia a la **criptografía visual** (*Visual Cryptography*) y a la idea de "apilar" (*stack*) ambas imágenes.

1. **Concepto de Criptografía Visual**:

   - En este esquema, una imagen secreta se divide en dos o más capas (imágenes) que de forma individual no revelan información (parecen ruido aleatorio/estático).

   - Sin embargo, al superponerlas ("apilarlas"), los patrones de píxeles interactúan cancelando el ruido y revelando el mensaje oculto.

2. **Operación matemática (Suma modular de píxeles)**:

   - Apilar digitalmente dos imágenes equivale a combinar sus matrices de píxeles mediante operaciones aritméticas o lógicas bit a bit.

   - Al realizar la suma modular canal por canal:

     $$\text{Píxel}_{\text{resultado}} = (\text{Píxel}_1 + \text{Píxel}_2) \pmod{256}$$

   - El ruido se cancela exactamente en un fondo blanco uniforme (`rgb(255, 255, 255)`), dejando al descubierto el texto de la bandera en color oscuro.

Bandera obtenida: `academy{2f16d0c4}`

## Notas Adicionales

- **Script en Python con Pillow y NumPy**:

  python

  from PIL import Image

  import numpy as np

  # Cargar ambas imágenes

  img1 = Image.open("scrambled1.png")

  img2 = Image.open("scrambled2.png")

  # Convertir a matrices numéricas para evitar desbordamiento antes del módulo

  arr1 = np.array(img1, dtype=np.uint16)

  arr2 = np.array(img2, dtype=np.uint16)

  # Sumar módulo 256

  res_arr = ((arr1 + arr2) % 256).astype(np.uint8)

  # Guardar y visualizar el resultado

  res_img = Image.fromarray(res_arr)

  res_img.save("flag_revealed.png")

- **Resolución con StegSolve**:
    - También es posible resolver este reto usando la herramienta clásica **StegSolve** (Java):
        1. Abrir `scrambled1.png`.
        2. Ir al menú `Analyse` -> `Image Combiner`.
        3. Seleccionar `scrambled2.png`.
        4. Cambiar entre modos de combinación (en este caso el modo `ADD`) hasta que el texto sea perfectamente legible.

## **Referencias**

- [Visual Cryptography (Wikipedia)](https://en.wikipedia.org/wiki/Visual_cryptography)
- [Pillow (PIL) ImageChops Module](https://pillow.readthedocs.io/en/stable/reference/ImageChops.html)
- [StegSolve Tool Guide](http://www.caesum.com/handbook/Stegsolve.jar)