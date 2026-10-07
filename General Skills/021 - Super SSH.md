# Descripcion
Using a Secure Shell (SSH) is going to be pretty important.
Can you `ssh` as `ctf-player` to `titan.picoctf.net` at port `51716` to get the flag?

You'll also need the password `84b12bae`. If asked, accept the fingerprint with `yes`.

If your device doesn't have a shell, you can use: [](https://webshell.picoctf.org/)[https://webshell.picoctf.org](https://webshell.picoctf.org/)

If you're not sure what a shell is, check out our Primer: [](https://primer.picoctf.com/#_the_shell)[https://primer.picoctf.com/#_the_shell](https://primer.picoctf.com/#_the_shell)
## Solucion
`raxel05-academy@webshell:~$ ssh ctf-player@titan.picoctf.net -p 51716`
`The authenticity of host '[titan.picoctf.net]:51716 ([3.139.174.234]:51716)' can't be established.`
`ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.`
`This key is not known by any other names`
`Are you sure you want to continue connecting (yes/no/[fingerprint])? yes`
`Warning: Permanently added '[titan.picoctf.net]:51716' (ED25519) to the list of known hosts.`
`ctf-player@titan.picoctf.net's password:` 
`Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_07a987ac}`
`Connection to titan.picoctf.net closed.`
`raxel05-academy@webshell:~$` 

## Notas Adicionales
+ ssh nos permite conectar a servidores remotos

## Referencias
+ https://linux.die.net/man/1/ssh

