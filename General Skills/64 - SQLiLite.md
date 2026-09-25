# Descripcion
Can you login to this website?

## Solucion
1. En el login, usar el usuario `admin' --` y contraseña vacía o cualquiera.
2. El `--` comenta el chequeo de contraseña en la query SQL.
3. Iniciar sesión correctamente.
4. Ver código fuente (Ctrl+U) para leer la flag en `<p hidden>`.

## Notas Adicionales
- Vulnerabilidad: SQL Injection (login bypass).
- Payload alternativo: `' OR 1=1--`.
- La flag está oculta en el HTML, no visible en pantalla.

## Referencias
- picoCTF 2022 - SQLiLite (Web, Medium) - Mubarak Mikail