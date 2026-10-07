# Descripcion
This website puts a two-factor prompt between you and the flag. Register an account, then take a close look at the requests your browser is actually sending.
  
## Solucion
1. Registrarse en la página con cualquier dato inventado.
2. Interceptar la petición POST que se envía al introducir el OTP (con Burp Suite o DevTools).
3. En el cuerpo de la petición, **eliminar por completo el parámetro `otp`** (no dejarlo vacío, borrar la clave entera).
4. Reenviar la petición modificada.
5. El servidor omite la verificación del OTP y devuelve la flag en la respuesta


## Notas Adicionales
- Tipo de vulnerabilidad: **Broken Authentication / Improper Input Validation**.
- El servidor valida con algo similar a `if otp: check_otp()`. Al no existir el parámetro, la condición es falsa y salta la verificación.
- Renombrar el campo (`otgp=1234`) o dejarlo vacío (`otp=`) **no** funciona; la clave está en eliminar la clave por completo.
- Herramientas útiles: Burp Suite (Proxy / Repeater) o DevTools del navegador (pestaña Network → Edit and Resend).

## Referencias
- Reto: picoCTF 2024 - IntroToBurp (Web Exploitation, Easy)
- Autores: Nana Ama Atombo-Sackey & Sabine Gisagara
- Categoría OWASP relacionada: A07:2021 – Identification and Authentication Failures
