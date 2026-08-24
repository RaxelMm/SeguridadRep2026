# Descripcion
Unzip this archive and find the file named 'uber-secret.txt'

## Solucion
`raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c/501/files.zip`
`raxel05-academy@webshell:~$ unzip files.zip` 
`raxel05-academy@webshell:~$ cd files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/`    
`raxel05-academy@webshell:~/files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets$ ls`
`uber-secret.txt`
`raxel05-academy@webshell:~/files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets$ cat uber-secret.txt` 
`picoCTF{f1nd_15_f457_ab443fd1}`
## Notas Adicionales
+ La propia terminal nos dice como llegar a ese directorio del archivo y le aplicamos un cat , llegamos mediante cd 
## Referencias
https://webshell.cylabacademy.org
