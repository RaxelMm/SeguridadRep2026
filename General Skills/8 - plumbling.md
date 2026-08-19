# Descripcion
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?
## Solucion
```
raxel05-academy@webshell:~$ nc fickle-tempest.picoctf.net 56696 | grep pico
picoCTF{digital_plumb3r_8c8f3412}
```
picoCTF{digital_plumb3r_8c8f3412}
## Notas Adicionales
+ Usando el comando netcat y la funcion grep para encontrar la bandera en todo el texto arrojado
## Referencias
https://webshell.cylabacademy.org

