# Descripción

Download this disk image and find the flag.

> Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://challenge-files.cylabacademy.net/library/c43b9c25ad2c97fb0c7c393a7b5f95065b79c0faf5848e1eeb6a453ec3e78f7d/disk.flag.img.gz)

## Solución

Primero se descarga y descomprime la imagen del disco en `/tmp`.

```
cd /tmp
wget https://challenge-files.cylabacademy.net/library/c43b9c25ad2c97fb0c7c393a7b5f95065b79c0faf5848e1eeb6a453ec3e78f7d/disk.flag.img.gz
gunzip disk.flag.img.gz
```

Una vez obtenida la imagen, se puede analizar su sistema de archivos utilizando herramientas de **The Sleuth Kit**.

El objetivo es encontrar archivos eliminados que puedan contener información relevante. Primero se identifica la estructura del sistema de archivos:

```
mmls disk.flag.img
```

El offset correspondiente al sistema de archivos es:

```
411648
```

Se puede utilizar `fls` para listar los archivos y directorios de la imagen:

```
fls -o 411648 disk.flag.img
```

Durante el análisis se encontraron dos inodes relevantes:

- `1782` → archivo cifrado de 64 bytes.
- `1875` → archivo que contiene un historial de comandos.

### Recuperar el historial de comandos

Se utiliza `icat` para extraer el contenido del inode `1875`:

```
icat -o 411648 disk.flag.img 1875
```

El contenido recuperado muestra los comandos ejecutados anteriormente:

```
touch flag.txt
nano flag.txt
apk get nano
apk --help
apk add nano
nano flag.txt
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt
```

Este historial revela información importante:

```
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
```

Por lo tanto:

- El archivo original era `flag.txt`.
- El archivo cifrado era `flag.txt.enc`.
- Se utilizó AES-256-CBC mediante `openssl aes256`.
- La contraseña utilizada fue `unbreakablepassword1234567`.
- Posteriormente, el archivo original fue eliminado mediante `shred -u`.

### Recuperar el archivo cifrado

El inode `1782` tiene un tamaño de 64 bytes y corresponde al archivo cifrado:

```
istat -o 411648 disk.flag.img 1782
```

Para recuperar su contenido:

```
icat -o 411648 disk.flag.img 1782 > flag.enc
```

Se puede comprobar que el archivo comienza con `Salted__`:

```
icat -o 411648 disk.flag.img 1782 | xxd
```

Salida relevante:

```
00000000: 5361 6c74 6564 5f5f ...
```

`Salted__` indica que OpenSSL almacenó una sal al principio del archivo cifrado.

### Descifrar el archivo

La contraseña encontrada en el historial es:

```
unbreakablepassword1234567
```

Por lo tanto, se intenta descifrar el archivo:

```
openssl enc -d -aes-256-cbc -in flag.enc -out flag.txt -pass pass:unbreakablepassword1234567
```

OpenSSL puede mostrar una advertencia sobre la derivación de claves antigua y, dependiendo de la versión utilizada, incluso mostrar `bad decrypt`. Sin embargo, se debe comprobar el contenido generado:

```
cat flag.txt
```

El resultado obtenido es:

```
academy{h4un71ng_p457_0cf3a06d}
```

### Flag

```
academy{h4un71ng_p457_0cf3a06d}
```

## Notas Adicionales

- `mmls` permite identificar las particiones y obtener el offset necesario para trabajar con el sistema de archivos dentro de la imagen.
- `fls` permite listar archivos y directorios dentro de una imagen forense.
- `icat` permite recuperar el contenido asociado a un inode específico.
- `istat` permite consultar información del inode, como tamaño, tiempos y bloques asociados.
- El inode `1875` fue especialmente importante porque contenía el historial de comandos utilizado para crear y eliminar el archivo.
- El comando `shred -u flag.txt` eliminó el archivo original, pero no impidió recuperar información relacionada con él desde la imagen.
- El archivo cifrado comenzaba con `Salted__`, indicando que fue generado utilizando la opción `-salt` de OpenSSL.
- La contraseña no tuvo que ser crackeada: fue encontrada directamente en el historial recuperado de la imagen.
- El comando original utilizó `openssl aes256`, que corresponde al cifrado AES-256-CBC.
- Las advertencias sobre `deprecated key derivation used` de OpenSSL 3.x no significan que el archivo original haya utilizado PBKDF2. El archivo fue creado utilizando la derivación de claves antigua compatible con el comando original.

## Referencias

- [The Sleuth Kit](https://www.sleuthkit.org/)
- [The Sleuth Kit Wiki](https://wiki.sleuthkit.org/)
- [OpenSSL Documentation](https://docs.openssl.org/)
- [Cyber Academy](https://challenge-files.cylabacademy.net/)