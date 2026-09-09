
# Descripcion
Find the flag being held on this server to get ahead of the competition
## Solucion
`marquez@marquez-VirtualBox:~/Escritorio$ curl -s -I  http://wily-courier.picoctf.net:53140/index.php`

`HTTP/1.1 200 OK`
`Date: Mon, 07 Sep 2026 16:24:16 GMT`
`Server: Apache/2.4.38 (Debian)`
`X-Powered-By: PHP/7.2.34`
`flag: picoCTF{r3j3ct_th3_du4l1ty_8b13f07}`
`Content-Type: text/html; charset=UTF-8`


## Notas Adicionales
- curl -s -I para acceder a las cabeceras de una pagina web
## Referencias


