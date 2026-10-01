# Descripcion

## Solucion
1. Verificar con `xxd -g 1 whitepages.txt` → dos patrones: `20` (espacio) y `e2 80 83` (EM SPACE).
2. Convertir a binario: EM SPACE = 0, espacio = 1.
3. Agrupar en bytes de 8 bits y convertir a ASCII.
4. Flag obtenida.
**Script:**
`python`
`with open('whitepages.txt', 'rb') as f:`
    `data = f.read()`
`bits = ''`
`i = 0`
`while i < len(data):`
    `if data[i:i+3] == b'\xe2\x80\x83':`
        `bits += '0'; i += 3`
    `elif data[i:i+1] == b'\x20':`
        `bits += '1'; i += 1`
    `else:`
        `i += 1`
`flag = ''`
`for j in range(0, len(bits), 8):`
    `if len(bits[j:j+8]) == 8:`
        `flag += chr(int(bits[j:j+8], 2))`
`print(flag)`


## Notas Adicionales
- Técnica: **Whitespace Steganography** (esteganografía con espacios).
    
- Dos espacios Unicode visualmente idénticos pero con bytes distintos.
    
- `strings` no sirve: los bytes `e2 80 83` no son imprimibles.
    
- Herramientas alternativas: CyberChef (reemplazar bytes → From Binary).
## Referencias
- picoCTF 2019 - WhitePages (Forensics, Medium)
