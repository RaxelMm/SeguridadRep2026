## Descripción 
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log. Download the encoded data here: [Logs Data](https://challenge-files.cylabacademy.net/library/c1d1cdbc5ff364586834283bcfd8a8d314aaecd2faef1cc08402f0ab3e4120d3/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .
## Solución 
```
academy{forensics_analysis_is_amazing_1c6b929d}
```
## Notas adicionales 
* Se identificó que el supuesto archivo de logs era un volcado de texto codificado en Base64. Se utilizó el comando `base64 -d logs.txt > imagen.png` en la terminal para revertir la codificación y reconstruir el archivo multimedia original. A partir de ahí, se inspeccionó la imagen resultante para extraer la bandera
## Referencias