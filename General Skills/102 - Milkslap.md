# Descripcion
🥛
## Solucion
1. Abrir el sitio del reto. Se ve una animación de un vaso de leche.
2. En DevTools (F12) → pestaña Network, recargar la página.
3. En el CSS (`milkslap-milkslap.scss`) aparece la referencia:
   css
   #image {
     background-image: url(concat_v.png);
   }

4. El archivo `concat_v.png` es un **sprite vertical** con todos los frames de la animación.
    
5. Descargar la imagen:
    
    powershell
    
    Invoke-WebRequest -Uri "http://chatelaine.cylabacademy.net:41442/concat_v.png" -OutFile "concat_v.png"
    
6. Al abrirla, se ve como una franja vertical larga (muy alta). La flag está dibujada en la parte inferior.
    
7. Cortar la parte de abajo con Python (Pillow):
    
    python
    
    from PIL import Image
    img = Image.open("concat_v.png")
    w, h = img.size
    print(f"Tamaño: {w} x {h}")
    Cortar el 10% inferior
    bottom = img.crop((0, int(h * 0.9), w, h))
    bottom.save("bottom.png")
    
8. Abrir `bottom.png` y leer la flag.
## Notas Adicionales
- **Categoría**: Forensics → análisis de imágenes/steganografía.
    
- Los sprites verticales contienen **todos los frames de una animación** apilados uno debajo de otro.
    
- El visor de Windows escala la imagen y hace invisible el detalle. Hay que cortarla o redimensionarla.
    
- La flag está **dibujada directamente** en la parte baja del sprite, no oculta en bits.
    
- Alternativa: abrir la URL de la imagen directamente en el navegador y hacer zoom (Ctrl+Scroll).
    
- Herramientas: Pillow (Python), GIMP, navegador con zoom, DevTools (Network).
    
- Flag: `picoCTF{imag3_m4n1pul4t10n_sl4p5}` (o `academy{...}` en CyLab).
    

## Referencias

