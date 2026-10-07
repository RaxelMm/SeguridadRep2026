# Descripcion
There's something in the [building](https://challenge-files.cylabacademy.net/library/5235bfccd8f3cc2d059ee828f774846542f28f7ec66cb4f0c6ceb536c38026d4/buildings.png). Can you retrieve the flag?
## Solucion
1. Descargar la imagen `buildings.png`.
2. Usar decodificador online de esteganografía (stylesuxx) o herramienta `zsteg`.
3. Con zsteg: `zsteg buildings.png` → muestra la flag directamente.
4. Con online: subir imagen, pulsar Decode, leer la flag.
## Notas Adicionales
- Técnica: Esteganografía LSB (Least Significant Bit).
- Cada canal de color (R, G, B) almacena 8 bits; modificar el último bit es invisible al ojo humano.
- `zsteg` es la herramienta correcta para PNG (steghide no sirve para PNG).
- La flag está oculta en `b1,rgb,lsb,xy` (bit 1, canal RGB, LSB, orden XY).
## Referencias

