

## Descripcion
Can you win in a convincing manner against this chess bot? He won't go easy on you!

## Solucion
1. Abrir el sitio del reto.
2. Abrir DevTools (F12) -> Console.
3. Enviar una evaluacion falsa extremadamente negativa:
   `sendMessage("eval -100000")`
4. El bot se rinde y muestra la flag.

## Notas Adicionales
- **Vulnerabilidad**: Client-side trust issue (WebSocket message manipulation).
- La funcion `sendMessage()` esta expuesta globalmente en el objeto `window`.
- El servidor confia en el valor `eval` enviado por el cliente sin validacion server-side.
- El umbral es `eval < -50000`; cualquier valor mas negativo funciona.
- Se puede usar `ws.send("eval -100000")` en lugar de `sendMessage()`.
- Herramientas: DevTools (Console), Burp Suite.

## Referencias
- picoCTF 2025 - WebSockFish (Web Exploitation, Medium)
- Flag: `picoCTF{c1i3nt_s1d3_w3b_s0ck3t5_dc1dbff7}`