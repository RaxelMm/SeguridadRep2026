## Descripción 
Can you abuse the oracle?

An attacker was able to intercept communications between a bank and a fintech company. They managed to get the [message](https://challenge-files.cylabacademy.net/library/c160444b2e2c0d9b093294670f0feec4d0e65abfcfc56e9524fb337c65cb9110/secret.enc) (ciphertext) and the [password](https://challenge-files.cylabacademy.net/library/c160444b2e2c0d9b093294670f0feec4d0e65abfcfc56e9524fb337c65cb9110/password.enc) that was used to encrypt the message. After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here `nc chatelaine.cylabacademy.net 36638`. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.
## Solución 
```
academy{su((3ss_(r@ck1ng_r3@_88a127f1}
```
## Notas adicionales 
* 
## Referencias