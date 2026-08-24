# Descripcion
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin.
## Solucion
`raxel05-academy@webshell:~$ ssh ctf-player@wily-courier.picoctf.net -p 54052`
`ctf-player@pico-chall$ ls`
`1of3.flag.txt  instructions-to-2of3.txt`
`ctf-player@pico-chall$ cat 1of3.flag.txt` 
`picoCTF{xxsh_`
`ctf-player@pico-chall$ cat instructions-to-2of3.txt` 
`Next, go to the root of all things, more succinctly /`
`ctf-player@pico-chall$ /`
`-bash: /: Is a directory`
`ctf-player@pico-chall$ cd /`
`ctf-player@pico-chall$ cd /`
`ctf-player@pico-chall$ ls`
`2of3.flag.txt  bin  boot  challenge  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var`
`ctf-player@pico-chall$ cd 2of3.flag.txt` 
`-bash: cd: 2of3.flag.txt: Not a directory`
`ctf-player@pico-chall$ cat 2of3.flag.txt` 
`0ut_0f_//4t3r_`
`ctf-player@pico-chall$ ^C`
`ctf-player@pico-chall$ ls`
`2of3.flag.txt  bin  boot  challenge  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var`
`ctf-player@pico-chall$ cat instructions-to-3of3.txt` 
`Lastly, ctf-player, go home... more succinctly ~`
`ctf-player@pico-chall$ cd ~`
`ctf-player@pico-chall$ ls`
`3of3.flag.txt  drop-in`
`ctf-player@pico-chall$ cat 3of3.flag.txt` 
`0b24fc4f}ctf-player@pico-chall$ Connection to wily-courier.picoctf.net closed by remote host.`
`Connection to wily-courier.picoctf.net closed.`
`raxel05-academy@webshell:~$` 
## Notas Adicionales
+ podemos entrar a la raiz mediante el / 
+ podemos entrar a home mediante un ~
## Referencias
https://webshell.cylabacademy.org

