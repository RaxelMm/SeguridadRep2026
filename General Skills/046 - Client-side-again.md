# Descripcion
Can you break into this super secure portal?
## Solucion
Construir los substrings del codigo fuente que nos da la bandera para poder obtenerla
## Paso 1: Identificar el diccionario

Al inicio aparece:

```
var _0x5a46 = [
  'daf93}', '_again_4', 'this',
  'Password Verified', 'Incorrect password',
  'getElementById', 'value', 'substring',
  'picoCTF{', 'not_this'
];
```

Esas son las palabras reales.

## Paso 2: Ver la rotación

Luego viene esta función:

```
(function(arr, n){
    while(--n){
        arr.push(arr.shift());
    }
}(_0x5a46, 0x1b3));
```

Hace un rotate del arreglo 434 veces (`0x1b3 = 435`, pero el `--n` deja 434).

Como el arreglo tiene 10 elementos:

434  10=4434 \bmod 10 = 4434mod10=4

O sea, rotó 4 posiciones.

El arreglo queda así:

|Índice|Valor|
|---|---|
|0|`getElementById`|
|1|`value`|
|2|`substring`|
|3|`picoCTF{`|
|4|`not_this`|
|5|`_again_4`|
|6|`daf93}`|
|7|`this`|
|8|`Password Verified`|
|9|`Incorrect password`|

## Paso 3: Sustituir los índices

La función:

```
_0x4b5b('0x3')
```

simplemente devuelve el elemento 3 del arreglo:

```
_0x4b5b('0x3') → "picoCTF{"
```

Entonces este código:

```
if(checkpass[_0x4b5b('0x2')](0,8)==_0x4b5b('0x3'))
```

se convierte en:

```
if (checkpass.substring(0,8) == "picoCTF{")
```

## Paso 4: Reconstruir la flag

Las demás condiciones aportan fragmentos:

```
substring(8,16)  = "not_this"
substring(16,24) = "_again_4"
substring(24,32) = "daf93}"
```

Uniéndolo:

```
picoCTF{not_this_again_4daf93}
```
## Notas Adicionales
+ Ofuscacion es un metodo para proteger datos 
## Referencias
+ http://fickle-tempest.picoctf.net:61168/

