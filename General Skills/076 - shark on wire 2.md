# Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/f76620763560ca0683be36e0ed4648743f969ab4d852fda0d8fb4d3ae21a173d/shark-on-wire-2-capture.pcap). Recover the flag that was pilfered from the network

## Solucion
1. Descargar el pcap del reto (`capture.pcap` o `shark-on-the-wire.pcap` según versión).
2. Filtrar paquetes UDP con puerto destino 22 (`dport == 22`).
3. Cada paquete de esa secuencia trae en su **puerto de origen** (`sport`) el valor `5000 + ASCII` de un carácter de la flag.
4. Restar 5000 a cada `sport` y convertir a carácter ASCII.
5. Extraer la flag del mensaje resultante con regex `picoCTF{.*?}`.

`**Script Python (scapy):**`
`python`
`import os, re`
`from scapy.all import rdpcap, UDP`
`os.chdir(r"C:\ruta\donde\esta\el\pcap")`
`paquetes = rdpcap("shark-on-the-wire.pcap")`
`mensaje = ""`
`for p in paquetes:`
    `if UDP in p and p[UDP].dport == 22:`
        `mensaje += chr(p[UDP].sport - 5000)`
`print(mensaje)`
`flag = re.search(r'picoCTF\{.*?\}', mensaje)`
`print("FLAG:", flag.group(0) if flag else "no encontrada")`

## Notas Adicionales
- Covert channel: la info viaja en los **puertos de origen UDP**, no en el payload.
    
- Rango de puertos ≈ `5032–5126` → `5000 + ASCII(32..126)`.
    
- El pcap incluye ruido (ráfagas de 'a') a propósito.
    
- Si `rdpcap` falla con `FileNotFoundError`, revisar `os.getcwd()` y usar `os.chdir()` o ruta absoluta.
    
- Alternativas sin scapy: `tshark -r capture.pcap -Y "udp.dstport==22" -T fields -e udp.srcport` y luego restar 5000.
    
- Flag: `picoCTF{p1LLf3r3d_data_v1a_st3g0}`

## Referencias
- picoCTF 2019 - shark on wire 2 (Forensics, Medium)
    
- Autor: Danny
    
- Herramientas: scapy, Wireshark, tshark
