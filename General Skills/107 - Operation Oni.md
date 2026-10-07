# Descripcion
Download this disk image, find the key and log into the remote machine.

> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download disk image](https://challenge-files.cylabacademy.net/library/bac64668d6b7caead36e15b7bfc362eeea2c831d367e655a082b9fe63bd85610/disk.img.gz)
- Remote machine:  
    `ssh -i key_file -p 29408 ctf-player@chatelaine.cylabacademy.net`

## Solución

### 1. Descargar y descomprimir la imagen

Primero se descarga la imagen del disco y se descomprime dentro de `/tmp`.

```
cd /tmp

wget https://challenge-files.cylabacademy.net/library/bac64668d6b7caead36e15b7bfc362eeea2c831d367e655a082b9fe63bd85610/disk.img.gz

gunzip disk.img.gz
```

### 2. Identificar las particiones

Se utiliza `mmls` para analizar la tabla de particiones:

```
mmls disk.img
```

Se encontraron dos particiones Linux:

```
Start       End        Length
2048        206847     204800
206848      471039     264192
```

La primera partición comienza en el sector `2048` y la segunda en `206848`.

### 3. Analizar la primera partición

Se utiliza `fls` para listar su contenido:

```
fls -o 2048 disk.img
```

El resultado mostró principalmente archivos relacionados con el arranque del sistema:

```
lost+found
ldlinux.sys
ldlinux.c32
config-virt
vmlinuz-virt
initramfs-virt
extlinux.conf
...
```

Por lo tanto, esta partición corresponde principalmente al sistema de **boot** y no parece contener la clave buscada.

### 4. Analizar la segunda partición

Se analiza la segunda partición utilizando su offset `206848`:

```
fls -o 206848 disk.img
```

Se encontró la estructura principal del sistema Linux:

```
home
boot
etc
proc
dev
tmp
lib
var
usr
bin
sbin
media
mnt
opt
root
run
srv
sys
```

La presencia de `/root` resulta especialmente interesante porque el objetivo es encontrar una clave SSH.

### 5. Revisar `/root`

El directorio `/root` corresponde al inode `470`.

```
fls -o 206848 disk.img 470
```

Se encontraron:

```
.ash_history
.ssh
```

El directorio `.ssh` es especialmente relevante porque normalmente contiene claves utilizadas para autenticación SSH.

### 6. Revisar `/root/.ssh`

El directorio `.ssh` corresponde al inode `3916`:

```
fls -o 206848 disk.img 3916
```

El resultado fue:

```
r/r 2345: id_ed25519
r/r 2346: id_ed25519.pub
```

Se encontró una clave privada `id_ed25519` y su correspondiente clave pública.

### 7. Recuperar la clave privada

La clave privada corresponde al inode `2345`, por lo que se recupera utilizando `icat`:

```
icat -o 206848 disk.img 2345 > key_file
```

Se comprobó que se trataba de una clave privada OpenSSH:

```
-----BEGIN OPENSSH PRIVATE KEY-----
```

Se cambian los permisos del archivo para que SSH permita utilizarlo:

```
chmod 600 key_file
```

### 8. Conectarse al servidor remoto

Utilizando la clave recuperada y los datos proporcionados por el reto:

```
ssh -i key_file -p 29408 ctf-player@chatelaine.cylabacademy.net
```

Después de aceptar la huella del servidor, se obtuvo acceso como:

```
ctf-player@challenge:~$
```

### 9. Encontrar la flag

Una vez dentro del servidor se listó el contenido del directorio personal:

```
ls -la
```

Se encontró:

```
-rw-r--r-- 1 root root 28 Sep 23 02:58 flag.txt
```

Aunque `flag.txt` pertenece a `root`, sus permisos permiten que otros usuarios puedan leerlo (`r--`).

Finalmente:

```
cat flag.txt
```

Esto muestra la flag del reto.

## Notas Adicionales

- `mmls` permite identificar las particiones de una imagen de disco y sus sectores de inicio.
- El valor obtenido como `Start` se utiliza como offset para las herramientas de The Sleuth Kit.
- `fls` permite listar archivos y directorios dentro de un sistema de archivos contenido en una imagen forense.
- `icat` permite recuperar el contenido de un archivo a partir de su inode.
- La primera partición correspondía principalmente a archivos de arranque.
- La segunda partición contenía el sistema Linux principal.
- La búsqueda de `/root/.ssh` permitió encontrar una clave privada SSH.
- `id_ed25519` es una clave privada SSH basada en el algoritmo Ed25519.
- El archivo `id_ed25519.pub` es la clave pública correspondiente.
- Después de recuperar la clave privada fue necesario utilizar `chmod 600` para establecer permisos adecuados para SSH.
- La clave recuperada permitió autenticarse como `ctf-player` en la máquina remota.
- Una vez dentro de la máquina, `flag.txt` podía ser leído porque, aunque pertenecía a `root`, tenía permisos de lectura para otros usuarios.

## Referencias

- [The Sleuth Kit](https://www.sleuthkit.org/)
- [The Sleuth Kit Wiki](https://wiki.sleuthkit.org/)
- [OpenSSH](https://www.openssh.com/)
- [picoCTF 2022](https://picoctf.org/)
- [Cyber Academy](https://challenge-files.cylabacademy.net/)
