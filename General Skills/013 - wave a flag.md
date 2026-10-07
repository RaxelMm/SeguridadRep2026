# Descripcion
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...
## Solucion
`raxel05-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_wily_courier/c293351e09ee53217c6a868e7f98a0a2ba0cf9cdc4e4ed0e18f685d47111c216/warm  raxel05-academy@webshell:~$ chmod +x warm  raxel05-academy@webshell:~$ ./warm -h`
`Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}` `
## Notas Adicionales
+ chmod +x agrega permisos de ejecucion a un binario en linux
+ /warm ejecuta el binario warm una vez que ya tiene los permisos de ejecucion
+ ELF es el formato de archivo ejecutable en linux (como el .EXE)
+ file me dice que tipo de archivo
## Referencias
+ yo soy un tryhard ,pero con chatgpt


