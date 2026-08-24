# Descripcion
Can you find the flag in [file](https://challenge-files.picoctf.net/c_fickle_tempest/563d66bbed3925c75ed71efa974bfafab26460ae99938d699a8881cd173fca60/strings) without running it?
## Solucion
Obtener el archivo mediante wget y usar el comando strings
`raxel05-academy@webshell:~$ strings strings | grep pico`
## Notas Adicionales
+ Strings: muestra las cadenas (caracteres) en un archivo binario (no texto)
## Referencias
https://webshell.cylabacademy.org

