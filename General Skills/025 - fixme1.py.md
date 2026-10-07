# Descripcion
Fix the syntax error in this Python script to print the flag.
## Solucion
`raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c/27/fixme1.py`
`raxel05-academy@webshell:~$ python fixme1.py`
  `File "/home/raxel05-academy/fixme1.py", line 20`
    `print('That is correct! Here\'s your flag: ' + flag)`
`IndentationError: unexpected indent`
`raxel05-academy@webshell:~$ nano fixme1.py` 
`raxel05-academy@webshell:~$ python fixme1.py`
`That is correct! Heres your flag: picoCTF{1nd3nt1ty_cr1515_182342f7}`
## Notas Adicionales
+ Python espera que todo este identado hacia la izquierda , si esta a la derecha es porque esta dentro de una funcion
+ nano -l me permite ver los numeros de linea y encontrar el error mas facil
## Referencias
+ https://webshell.cylabacademy.org

