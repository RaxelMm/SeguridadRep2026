# Descripcion
Find the flag in this [picture](https://challenge-files.cylabacademy.net/library/7d12ed78e80c80afccae7ae860ed2277f044812e86c7267efbf7e0200fc9fd1e/pico_img.png).

## Solucion
`marquez@marquez-VirtualBox:~/Escritorio$ wget https://challenge-files.cylabacademy.net/library/7d12ed78e80c80afccae7ae860ed2277f044812e86c7267efbf7e0200fc9fd1e/pico_img.png`
`--2026-09-28 10:40:50--  https://challenge-files.cylabacademy.net/library/7d12ed78e80c80afccae7ae860ed2277f044812e86c7267efbf7e0200fc9fd1e/pico_img.png`
`Resolviendo challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)... 13.226.187.37, 13.226.187.22, 13.226.187.66, ...`
`Conectando con challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)[13.226.187.37]:443... conectado.`
`Petición HTTP enviada, esperando respuesta... 200 OK`
`Longitud: 108795 (106K) [application/octet-stream]`
`Guardando como: ‘pico_img.png’`

`pico_img.png        100%[===================>] 106.25K   400KB/s    en 0.3s`    

`2026-09-28 10:40:51 (400 KB/s) - ‘pico_img.png’ guardado [108795/108795]`

`marquez@marquez-VirtualBox:~/Escritorio$ strings -n 10 pico_img.png` 
`tEXtSoftware`

## Notas Adicionales
+  El comando `strings` en Linux sirve para extraer secuencias de caracteres legibles (texto imprimible) de archivos que no son de texto, como archivos binarios, ejecutables o bibliotecas.

## Referencias

