# Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/webnet1-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/picopico.key). Recover the flag.

## Solucion
Para resolver este reto de análisis forense, se nos proporcionan dos archivos: una captura de red cifrada (`webnet1-capture.pcap`) y una clave privada RSA (`picopico.key`).

1. Al igual que en WebNet0, utilizamos la clave privada RSA para descifrar la sesión TLS del tráfico de red.

2. Analizando los paquetes descifrados (capa de aplicación), notamos un cambio: el encabezado HTTP `Pico-Flag` que antes contenía la bandera, ahora muestra el mensaje `academy{this.is.not.your.flag.anymore}` (una bandera falsa o señuelo).

3. Siguiendo con la inspección del tráfico HTTP en texto claro (revisando el contenido/cuerpo de las respuestas de otros archivos solicitados, como imágenes o estilos), logramos encontrar la verdadera bandera inyectada dentro de uno de los archivos transmitidos.

Bandera obtenida: `academy{honey.roasted.peanuts}`
## Notas Adicionales
- **Resolución con Wireshark**:

- Ve a `Editar > Preferencias > Protocolos > TLS`.

- En *RSA keys list* configura la IP del servidor, el puerto (443), el protocolo (http) y la ruta al archivo `picopico.key`.

- Una vez descifrado el tráfico, puedes buscar dentro de los paquetes (`Ctrl+F` -> String -> "academy{") o bien ir a `Archivo > Exportar Objetos > HTTP` para extraer y analizar todos los archivos transferidos (como las imágenes, donde se encuentra la bandera).

- **Resolución con Python**: También es posible resolverlo de manera programática mediante un script usando la librería `scapy` (inyectando la llave RSA a la sesión de capa TLS) y el módulo `cryptography`, e iterando sobre los datos de la capa de aplicación buscando expresiones regulares.
## Referencias

