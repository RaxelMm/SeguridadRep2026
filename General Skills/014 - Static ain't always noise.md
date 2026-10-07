# Descripcion
+ Can you look at the data in this binary? The bash script might help!
## Solucion
`raxel05-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_wily_courier/418e2775a501eaabeb99a96c5c467a83539369fe9649e8234644250cfb72d717/static`
`raxel05-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_wily_courier/418e2775a501eaabeb99a96c5c467a83539369fe9649e8234644250cfb72d717/ltdis.sh`
`raxel05-academy@webshell:~$ ./ltdis.sh static`
`raxel05-academy@webshell:~$ cat static.ltdis.strings.txt | grep pico`
   `3020 picoCTF{d15a5m_t34s3r_20335e41}`
## Notas Adicionales
+ un archivo sh es un archivo bach , contiene comandos linux agrupados
+ rm -rf borra archivos y carpetas dentro de la carpeta actual sin preguntar
## Referencias

