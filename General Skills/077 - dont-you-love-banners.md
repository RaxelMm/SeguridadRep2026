# Descripción 
Can you abuse the banner?

The server has been leaking some crucial information on `tethys.picoctf.net 49701`. Use the leaked information to get to the server.

To connect to the running application use `nc tethys.picoctf.net 54338`. From the above information abuse the machine and find the flag in the /root directory.
# Solución
academy{b4nn3r_gr4bb1n9_su((3sfu11y_b3ee718e}
# Notas adicionales
- El servicio muestra un "banner" al conectarse, que se lee del archivo `/home/player/banner`

- Al reemplazar ese archivo con un **enlace simbólico** a `/root/flag.txt`, el programa (que se ejecuta con privilegios elevados) lee el flag en lugar del banner original  

- Es una técnica clásica de **path traversal mediante symlinks** para leer archivos restringidos
## Referencias

