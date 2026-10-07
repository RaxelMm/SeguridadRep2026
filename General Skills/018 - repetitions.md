# Descripcion
Can you make sense of this file?
## Solucion
`raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c/476/enc_flag`
`raxel05-academy@webshell:~$ cat enc_flag | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d`
`picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_4557ec3e}`
## Notas Adicionales
- Usamos decode multiples veces hasta encontrar la bandera 
- Se usa decode en base64
## Referencias
+ https://askubuntu.com/questions/178521/how-can-i-decode-a-base64-string-from-the-command-line
+  Gemini



