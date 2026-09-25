# Descripcion
The flag is somewhere on this web application not necessarily on the website
## Solucion
1. Acceder al archivo de reconocimiento: `http://<instance>/robots.txt`
2. Analizar el contenido. Contiene varias cadenas ofuscadas, algunas en Base64 y otras basura:
     `User-agent *`  
`Disallow: /cgi-bin/`  
`Think you have seen your flag or want to keep looking.`

`ZmxhZzEudHh0;anMvbXlmaW`  
`anMvbXlmaWxlLnR4dA==`  
`svssshjweuiwl;oiho.bsvdaslejg`  
`Disallow: /wp-admin/`

## Notas Adicionales
+ Usar decodificacion base64

## Referencias

