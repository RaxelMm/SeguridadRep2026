# Descripcion
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.

To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!
## Solución

En este reto se nos proporciona una captura de tráfico de red llamada `myNetworkTraffic.pcap`. Las pistas nos indican que el intruso actuó de forma ordenada en el tiempo (*"in timely manner"*, *"time is essential"*) y que debemos ordenar/filtrar los paquetes.

1. **Inspección de la captura**:

   - La captura contiene solo 22 paquetes TCP SYN enviados desde `10.200.0.2:20` hacia `192.168.1.2:80`.

   - Cada paquete lleva una pequeña carga útil (*payload*) codificada en Base64.

   - En el archivo PCAP original, los paquetes se encuentran desordenados cronológicamente.

2. **Ordenar por tiempo (*Timestamp*)**:

   - Al ordenar los paquetes de forma cronológica estricta por su columna de tiempo (`Time`), observamos que los últimos 7 paquetes fueron enviados con intervalos de tiempo regulares y contienen fragmentos de texto legible en Base64:

     - `YWNhZGVteQ==`  -> `academy`

     - `ezF0X3c0cw==`  -> `{1t_w4s`

     - `bnRfdGg0dA==`  -> `nt_th4t`

     - `XzM0c3lfdA==`  -> `_34sy_t`

     - `YmhfNHJfYQ==`  -> `bh_4r_a`

     - `ODEzOWE0MQ==`  -> `8139a41`

     - `fQ==`          -> `}`

3. **Reconstrucción**:

   - Al concatenar las partes obtenidas en orden temporal, se forma la bandera completa: `academy{1t_w4snt_th4t_34sy_tbh_4r_a8139a41}`.

Bandera obtenida: `academy{1t_w4snt_th4t_34sy_tbh_4r_a8139a41}`

## Notas Adicionales

- **Resolución en Wireshark**:

  - Abre `myNetworkTraffic.pcap` en Wireshark.

  - Haz clic en el encabezado de la columna **Time** para ordenar los paquetes en orden cronológico ascendente.

  - Observa los últimos paquetes hacia el final de la captura y decodifica las cadenas Base64 presentes en el campo de datos TCP (*TCP Payload*).

- **Resolución con Python y Scapy**:

  python

  import base64

  import scapy.all as scapy

  pkts = sorted(scapy.rdpcap("myNetworkTraffic.pcap"), key=lambda p: p.time)

  flag = ""

  for p in pkts:

      payload = bytes(p[scapy.TCP].payload)

      try:

          decoded = base64.b64decode(payload).decode("ascii")

          flag += decoded

      except Exception:

          pass

  print("Bandera:", flag)

- **Técnica de exfiltración de datos**: El atacante utilizó paquetes TCP SYN con payloads anómalos (técnica de túnel encubierto o _covert channel_) mezclados con tráfico señuelo para exfiltrar datos de forma sigilosa.

## **Referencias**

- [Wireshark User's Guide - Sorting & Filtering Packets](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html)
- [Scapy Documentation - Packet Manipulation](https://scapy.readthedocs.io/en/latest/)
- [Covert Channels over TCP/IP](https://en.wikipedia.org/wiki/Covert_channel)

