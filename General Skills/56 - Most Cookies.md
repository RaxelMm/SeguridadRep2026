# Descripcion
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
## Solucion
Para resolver el reto se explotó la debilidad en la generación de la `SECRET_KEY` de Flask realizando un ataque de fuerza bruta fuera de línea (_offline brute force_) para forjar un token de administrador:

1. **Decodificación e Inspección:** Al acceder al sitio web, el servidor asigna una cookie de sesión cifrada/firmada mediante `itsdangerous`. Las cookies de sesión estándar de Flask están firmadas por HMAC pero no encriptadas, permitiendo leer su contenido interno.
    
2. **Fuerza Bruta a la Clave Secreta (`SECRET_KEY`):** Se utilizó la herramienta `flask-unsign` para verificar la firma de la cookie recibida contra la lista reducida de nombres de galletas proporcionada por la aplicación. La clave válida fue identificada correctamente.
    
3. **Falsificación de Sesión (_Session Forgery_):** Con la `SECRET_KEY` recuperada, se firmó un nuevo objeto de sesión estableciendo el parámetro de autenticación con privilegios elevados:
	1. {"very_auth": "admin"}
4. **Explotación y Exfiltración:** Se envió una nueva petición HTTP GET al endpoint `/display` pasando la cookie de sesión falsificada en la cabecera `Cookie: session=<payload_firmado>`, lo que permitió derivar los privilegios de acceso y obtener la bandera del reto.

## Notas Adicionales
- **Causa Raíz:** Uso de claves secretas predecibles, cortas o en listas de palabras públicas (`hardcoded/predictable secret keys`) para la firma de tokens de sesión.
    
- **Seguridad en Flask:** Aunque la firma criptográfica evita que el usuario altere arbitrariamente los datos de la sesión, si la `SECRET_KEY` es descubierta, un atacante gana la capacidad de firmar y validar cualquier identidad de manera arbitraria.
## Referencias
https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html?utm_source=gemini
https://www.google.com/search?q=https://flask.palletsprojects.com/en/stable/quickstart/%2523sessions&utm_source=gemini

