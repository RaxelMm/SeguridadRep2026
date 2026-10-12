# Descripcion
Can you get the real meaning from this file.
## Solucion
1. Descargar el archivo `enc_flag` y ver su contenido:
   cat enc_flag
   Salida:
   YidhR3BvYTJ4MFpudHFhR3g2YUhsZmF6TnFlVGwzWVROclh6Z3lNalF6TURrM2ZRPT0nCg==
2. Decodificar en Base64:
   cat enc_flag | base64 -d
   Salida:
   b'aGpoa2x0ZntqaGx6aHlfazNqeTl3YTNrXzgyMjQzMDk3fQ=='
3. Limpiar el prefijo b'' y decodificar otra vez en Base64:
   echo "aGpoa2x0ZntqaGx6aHlfazNqeTl3YTNrXzgyMjQzMDk3fQ==" | base64 -d
   Salida:
   hjhkltf{jhlzhy_k3jy9wa3k_82243097}
4. El resultado aun esta cifrado con ROT. Probar ROT19 (o usar CyberChef con ROT13 y ajustar Amount a 19):
   Entrada: hjhkltf{jhlzhy_k3jy9wa3k_82243097}
   Amount: 19
   Salida: academy{caesar_d3cr9pt3d_82243097}
5. La flag final es:
   academy{caesar_d3cr9pt3d_82243097}
## Notas Adicionales
- **Categoria**: Cryptography -> Codificaciones multiples.
- **Pasos de decodificacion**:
  1. Base64 (contenido del archivo)
  2. Base64 (resultado con prefijo b'')
  3. ROT19 (cifrado Cesar con desplazamiento 19)
- El prefijo `b''` en Python indica un **byte string**. Al pasar el output de `base64 -d` a un segundo `base64 -d`, hay que quitar el `b'` y el `'` final.
- ROT19 es una variante del cifrado Cesar donde cada letra se desplaza 19 posiciones hacia atras.
- Herramientas:
  - `base64 -d` (terminal)
  - CyberChef (operaciones From Base64 + ROT13 con Amount 19)
  - Python (base64.b64decode)
- Flag: academy{caesar_d3cr9pt3d_82243097}
## Referencias
- picoCTF 2024 - interencdec (Cryptography, Easy)
- Autor: NGIRIMANA Schadrack