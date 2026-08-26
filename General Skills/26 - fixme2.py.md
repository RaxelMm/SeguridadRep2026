# Descripcion
Fix the syntax error in the Python script to print the flag.
## Solucion
`raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c/6/fixme2.py`
`raxel05-academy@webshell:~$ python fixme2.py` 
  `File "/home/raxel05-academy/fixme2.py", line 22`
    `if flag = "":`
       `^^^^^^^^^`
`SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?`
`raxel05-academy@webshell:~$ nano fixme2.py` 
`raxel05-academy@webshell:~$ python fixme2.py` 
`That is correct! Here's your flag: picoCTF{3qu4l1ty_n0t_4551gnm3nt_f6a5aefc}`

## Notas Adicionales
+ el simbolo = en python o programacion , tiene un uso distino si se usa uno solo o dos consecutivos uno es compartativo y otro es para inicializar una variable
## Referencias
+ https://webshell.cylabacademy.org

