# Descripcion
Class, take your seats! It's PRIME-time for a quiz... `nc chatelaine.cylabacademy.net 27103`
## Solucion
Conectar: nc chatelaine.cylabacademy.net 37136
### Formulas RSA
- n = p * q
- phi(n) = (p-1)(q-1)
- d = e^(-1) mod phi(n)
- c = m^e mod n
- m = c^d mod n
### Casos resueltos
1. p, q → n: n = p*q  (Y)
2. p, n → q: q = n/p  (Y)
3. n grande, e=3 → p, q: no viable factorizar (N)
4. p, q → totient: phi = (p-1)(q-1)  (Y)
5. e, m, n → c: c = pow(m,e,n)  (Y)
6. e, c, n → m: no viable sin d (N)
7. e, p, q → d: d = inverse(e, (p-1)(q-1))  (Y)
8. e, p, n, c → m: q=n//p; d=inverse(e,(p-1)(q-1)); m=pow(c,d,n)  (Y)
### Script auxiliar
python
from Crypto.Util.number import inverse
q = n // p
phi = (p-1)*(q-1)
d = inverse(e, phi)
m = pow(c, d, n)

### Error comun

Si el reto pide un valor numerico despues de Y/N, hay que enviar el NUMERO, no otra "y". Si solo se manda "y", sale "Bad input, Exiting".

academy{wA8_th4t$_ill3aGal..oCFc4DC2a}

## Notas Adicionales

- Categoria: Cryptography -> RSA (asimetrico).
    
- Solo es viable cuando tienes p y q (o p y n, ya que q=n/p).
    
- No es viable factorizar un n grande.
    
- Herramientas: nc, Python (pycryptodome).
    

## Referencias

- picoCTF 2022 - RSA Oracle (Cryptography, Medium)