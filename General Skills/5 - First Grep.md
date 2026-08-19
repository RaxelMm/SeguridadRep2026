# Descripcion
Can you find the flag in the file? This would be really tedious to look through manually, something tells me there is a better way.
## Solucion
```
raxel05-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_fickle_tempest/2e9bfa4e1d90ac25a999fefdfb4feb8a2ff4eb73e4c61af4889a3762687ada01/file
raxel05-academy@webshell:~$ cat file | grep pico 
```
picoCTF{grep_is_good_to_find_things_29f42460}
## Notas Adicionales
la funcion grep ayuda a encontrar cadenas dentro de archivos
## Referencias
https://webshell.cylabacademy.org

