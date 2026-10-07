# Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/webnet1-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/picopico.key). Recover the flag.


## Solucion
Para resolver este reto de análisis forense, se nos proporcionan dos archivos: una captura de red cifrada (`webnet0-capture.pcap`) y una clave privada RSA (`picopico.key`). El objetivo es descifrar el tráfico de la captura utilizando dicha clave.

1. Se utiliza la clave privada RSA para descifrar la sesión TLS del tráfico de red.

2. Al analizar los paquetes en texto claro (capa de aplicación), se logra ver el intercambio de tráfico HTTP.

3. El servidor devuelve la bandera en texto claro inyectada dentro de un encabezado HTTP personalizado llamado `Pico-Flag` en sus respuestas.

Bandera obtenida: `academy{nongshim.shrimp.crackers}`
## Notas Adicionales
- **Resolución con Wireshark**: Puedes descifrar el tráfico en la interfaz gráfica yendo a `Editar > Preferencias > Protocolos > TLS`. Allí, seleccionas *RSA keys list* y configuras la IP del servidor, el puerto (443), el protocolo (http) y la ruta al archivo `picopico.key`.

- **Resolución con Python**: También es posible extraerlo de manera programática mediante un script con la librería `scapy` (cargando la capa `tls` e inyectando la llave RSA a la sesión) y el módulo `cryptography`.

- **Limitación de seguridad**: Esta técnica de descifrado con clave privada solo funciona porque la sesión TLS utilizaba intercambio de claves RSA. No es posible realizar esto en tráficos modernos configurados con *Perfect Forward Secrecy* (como ECDHE o DHE), los cuales requieren el registro de llaves de sesión (SSLKEYLOGFILE).
## Referencias

