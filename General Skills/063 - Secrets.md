# Descripcion
We have several pages hidden. Can you find the one with the flag?
## Solucion
1. Ver código fuente de `/` → referencia a `secret/assets/`.
2. Navegar a `/secret/` → "Finally. You almost found me."
3. Ver código fuente → referencia a `hidden/file.css`.
4. Navegar a `/secret/hidden/` → formulario falso.
5. Ver código fuente → referencia a `superhidden/login.css`.
6. Navegar a `/secret/hidden/superhidden/` → flag oculta con CSS.
7. `Ctrl+A` o ver código fuente para leerla.
## Notas Adicionales
- Pista "folders folders folders" → enumeración de directorios anidados.
- Flag oculta con CSS (texto blanco sobre blanco).
- Herramientas: DevTools, `wget -m`, `gobuster`.
## Referencias
- picoCTF 2022 - Secrets (Web, Medium) - Geoffrey Njogu