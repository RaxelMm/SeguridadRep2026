# Descripcion
Unzip this archive and find the flag.
## Solucion
raxel05-academy@webshell:~$ wget https://artifacts.picoctf.net/c/503/big-zip-files.zip
raxel05-academy@webshell:~$ unzip big-zip-files.zip 
raxel05-academy@webshell:~$ grep -ri pico ./big-zip-files 
./big-zip-files/folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
## Notas Adicionales
+ se aplica grep 
+ -r para forma recursiva 
+ -i para la carpeta que se selecciona
## Referencias
+ Gemini

