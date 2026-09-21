# Descripcion
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?
## Solucion
 
Con Burp enviar la peticion al repeater y vulnerar el XML para acceder al etc passwd
picoCTF{XML_3xtern@l_3nt1t1ty_540f4f1e}
## Notas Adicionales
+ Al aceptar la cabecera `Content-Type: application/xml` y procesar el cuerpo XML suministrado en `<data><ID>3</ID></data>`, el parser XML del backend probablemente no tiene deshabilitadas las entidades externas.
## Referencias
	https://gemini.google.com/app/bd80b3365db5af45?hl=es

