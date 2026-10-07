# Descripcion
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?
## Solucion
`raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c_titan/71/challenge.zip`
`raxel05-academy@webshell:~/drop-in$ git init`
`Reinitialized existing Git repository in /home/raxel05-academy/drop-in/.git/`
`raxel05-academy@webshell:~/drop-in$ git log` 
`raxel05-academy@webshell:~/drop-in$ git branch -a` 
`raxel05-academy@webshell:~/drop-in$ git checkout feature/part-1`
`Switched to branch 'feature/part-1'`
`raxel05-academy@webshell:~/drop-in$ cat flag.py` 
`print("Printing the flag...")`
`print("picoCTF{t3@mw0rk_", end='')raxel05-academy@webshell:~/drop-in$ git checkout feature/part-2`
`Switched to branch 'feature/part-2'`
`raxel05-academy@webshell:~/drop-in$ cat flag.py` 
`print("Printing the flag...")`

`print("m@k3s_th3_dr3@m_", end='')raxel05-academy@webshell:~/drop-in$ git checkout feature/part-3`
`Switched to branch 'feature/part-3'`
`raxel05-academy@webshell:~/drop-in$ cat flag.py` 
`print("Printing the flag...")`

`print("w0rk_4c24302f}")`
`raxel05-academy@webshell:~/drop-in$` 
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_4c24302f}
## Notas Adicionales
+ podemos ver las ramas locales mediante el git branch -a
+ con un checkout revisar cada uno y pudimos armar la bandera
## Referencias

https://medium.com/@vgqxjb/collaborative-development-9c1875e7dce2