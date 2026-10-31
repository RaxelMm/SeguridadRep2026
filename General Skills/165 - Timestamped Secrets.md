## Descripción 
Someone encrypted a message using AES in ECB mode but they weren’t very careful with their key. Turns out it’s derived from something as simple as the current time! Can you uncover the key and decrypt the flag? Download the encrypted message: [message](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/message.txt)  
You may also find the encryption script helpful: [code](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/encryption.py)
## Solución 
```
academy{sa3S_sEc9t_3b464909}
```
## Notas adicionales 
* descifrar un texto cifrado con AES-ECB cuya llave criptográfica era vulnerable: se derivaba de los primeros 16 bytes de un hash SHA-256 del timestamp exacto (tiempo UNIX en segundos) de su ejecución
## Referencias