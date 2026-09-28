
# Descripcion
This is a really weird text file. Can you find the flag? Get the flag from [TXT](https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt).
## Solucion
1. Ejecutar `file flag.txt` → revela que es una imagen PNG, no un texto.
2. Renombrar: `mv flag.txt flag.png`
3. Abrir la imagen con un visor (`eog`, `feh`, navegador).
4. La flag aparece escrita en la imagen.
## Notas Adicionales
- Los sistemas operativos usan **magic numbers** (firma de bytes) para identificar el tipo real, no la extensión.
    
- PNG siempre empieza con `89 50 4E 47` (‰PNG).
    
- `strings` no sirve aquí porque la flag está dibujada en la imagen, no como texto plano.
## Referencias

