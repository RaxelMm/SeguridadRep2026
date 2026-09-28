# Descripcion
We found this [packet capture](https://challenge-files.cylabacademy.net/library/e64f2c2aaf9bf531af7be1787c1407c47a4cc7b57f251d5108a1151e9721a2d6/shark-on-wire-1-capture.pcap). Recover the flag.
## Solucion
1. Descargar el archivo `shark-on-wire-1-capture.pcap`.
2. Instalar scapy: `pip3 install scapy --break-system-packages`
3. Ejecutar script en Python para extraer la flag de los paquetes UDP:
## Notas Adicionales
- Cada carácter de la flag viaja en un paquete UDP individual.
    
- El pcap contiene ruido: SSDP, SMB, ráfagas de `AAAA...`, `zzzz...`, `ffff...` y `fjdsakf;lankeflksanlkfdn`.
    
- Filtro clave: payload de **1 byte ASCII imprimible** (`32 <= byte < 127`).
    
- El truco del reto es descartar duplicados consecutivos para quedarse con la flag.
## Referencias

