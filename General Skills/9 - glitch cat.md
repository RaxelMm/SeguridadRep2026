# Descripcion
Our flag printing service has started glitching!
## Solucion
```
raxel05-academy@webshell:~$ nc saturn.picoctf.net 58779         
'picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}'
raxel05-academy@webshell:~$ python
>>> 'picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}'
'picoCTF{gl17ch_m3_n07_a4392d2e}'
```
picoCTF{gl17ch_m3_n07_a4392d2e}
## Notas Adicionales
+ Python utiliza los + para concatenar cadenas
+ chr() es una funcion de python que convierte un numero a su correspondiente caracter ASCII
+ solo es una suma de cadenas
## Referencias
https://webshell.cylabacademy.org

