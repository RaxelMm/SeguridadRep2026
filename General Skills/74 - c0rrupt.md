# Descripcion
We found this [file](https://challenge-files.cylabacademy.net/library/8388ecc430588d15064755583476bec46e23d42a6d8de6e8995c19e40f2e4c58/c0rrupt-mystery). Recover the flag.
## Solucion
1. `file c0rrupt-mystery` → devuelve "data" (formato no reconocido).
2. `xxd -g 1 c0rrupt-mystery | head` → firma PNG corrupta.
   - Empieza con `89 65 4e 34 0d 0a b0 aa` en vez de `89 50 4e 47 0d 0a 1a 0a`.
   - Nombre del IHDR corrupto: `43 22 44 52` (`C"DR`) en vez de `49 48 44 52` (`IHDR`).
3. Aplicar parches con script de Python:
   `python`
   `from pathlib import Path`
   `datos = bytearray(Path("c0rrupt-mystery").read_bytes())`
   `datos[0x00:0x08] = bytes.fromhex("89 50 4e 47 0d 0a 1a 0a")  # firma`
   `datos[0x0C:0x10] = b"IHDR"                                    # nombre`
   `datos[0x46] = 0x00                                            # quitar AA`
   `datos[0x4F:0x53] = bytes.fromhex("38 d8 2c 82")               # CRC pHYs`
   `datos[0x53:0x57] = bytes.fromhex("00 00 ff a5")               # long IDAT`
   `datos[0x57:0x5B] = b"IDAT"                                    # nombre IDAT`
   `Path("c0rrupt-fixed.png").write_bytes(datos)`

4. `pngcheck -v c0rrupt-fixed.png` → `No errors detected`.
    
5. Abrir la imagen y leer la flag.
## Notas Adicionales
- Concepto: reparación de PNG corrupto (magic bytes + chunks + CRC).
    
- Estructura PNG: firma (8 bytes) + chunks (longitud + tipo + datos + CRC).
    
- `file` solo mira los primeros bytes, no detecta corrupción interna.
    
- `pngcheck` es la herramienta correcta para validar PNG.
    
- Los offsets del archivo original eran: `0x00`, `0x0C`, `0x46`, `0x4F`, `0x53`, `0x57`.
    
- Flag: `academy{c0rrupt10n_1847995}`
## Referencias
- picoCTF 2019 - c0rrupt (Forensics, Medium)
    
- Herramientas: xxd, pngcheck, Python (pathlib)

