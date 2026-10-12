# Descripcion
Decrypt this message. Message: [message](https://challenge-files.cylabacademy.net/library/297f472a962ab45ee79af5ff4d616ba5206c85d5f4f5cfd41109602354d4121a/data.enc)
  
## Solucion
1. El reto proporciona un mensaje cifrado con el cifrado Cesar.
2. Se utiliza CyberChef (o cualquier herramienta de ROT) para probar diferentes desplazamientos.
3. Con un desplazamiento de 5 (ROT5) se obtiene el texto descifrado:
   crossingtherubiconfzpqvegy
4. La parte significativa es "crossingtherubicon", que corresponde a la flag.
5. La flag final es: picoCTF{crossingtherubicon}
## Notas Adicionales
- **Categoria**: Cryptography -> Cifrado clasico.
- **Cifrado Cesar**: Consiste en desplazar cada letra del alfabeto un numero fijo de posiciones.
- El desplazamiento correcto para este reto es 5.
- El texto extra "fzpqvegy" probablemente proviene de caracteres adicionales en el ciphertext original o de un error al copiar.
- Herramientas: CyberChef (operacion ROT13 con Amount 5), dCode, Python.
- Flag: picoCTF{crossingtherubicon}
## Referencias
- picoCTF 2019 - caesar (Cryptography, Medium)
- Autor: Sanjay C/Daniel Tunitis
