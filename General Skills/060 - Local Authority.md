## Solucion

1. Ir al portal: `http://xebec.cylabacademy.net:43984`
2. Observar el mensaje del formulario: *"Only letters and numbers allowed for username and password."* — pista de que la validación está en el cliente.
3. El formulario apunta a `login.php` con método POST.
4. Abrir directamente el login y ver el código fuente:
   `http://xebec.cylabacademy.net:43984/login.php`
5. En el HTML aparece la referencia a `secure.js`. Abrirlo:
   `http://xebec.cylabacademy.net:43984/secure.js`
6. Dentro de `secure.js` se encuentra la función `checkPassword()` con credenciales hardcodeadas:
   - usuario: `admin`
   - contraseña: `strongPassword098765`
1. Introducir esas credenciales en el formulario → redirige a `admin.php` → flag visible.

## Notas Adicionales
- Vulnerabilidad: **Client-Side Authentication / Sensitive Data Exposure**.
- El servidor delega la validación al navegador mediante `secure.js`, por lo que el código de verificación es público y las credenciales quedan expuestas en texto plano.
- basta con abrir `secure.js` directamente en el navegador y leer las credenciales.
- La flag (`j5_15_7r4n5p4r3n7`) se lee como **"JS is transparent"**, reforzando la lección de que el código del lado cliente no protege nada.
- Diferencia con IntroToBurp: aquí no se modifica la petición, se lee el código fuente del cliente.

## Referencias
- Reto: picoCTF 2022 - Local Authority (Web Exploitation, Easy)
- Autor: LT 'syreal' Jones
- Categoría OWASP: A07:2021 – Identification and Authentication Failures / A02:2021 – Cryptographic Failures

