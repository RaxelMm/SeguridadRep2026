# Descripcion
I found a web app that can help process images: PNG images only!
## Solucion
+ **Captura y Análisis:** Se interceptó la petición HTTP enviada por la aplicación, la cual utiliza una estructura XML simple:
```
<?xml version="1.0" encoding="UTF-8"?><data><ID>3</ID></data>
```
+ **Construcción del Payload:** Se definió una entidad externa personalizada (`&xxe;`) haciendo referencia al esquema de archivos locales del servidor (`file:///etc/passwd`).
+ **Inyección y Explotación:** Se sustituyó el cuerpo de la petición por el payload modificado:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
```
+ Obtención de la Bandera:** Al procesar la solicitud, el servidor resolvió la entidad externa e incluyó el contenido del archivo solicitado en la respuesta HTTP, revelando la bandera almacenada en el sistema.
## Notas Adicionales
+ Configuración insegura por defecto en la librería de parseo XML del backend (como `libxml_disable_entity_loader(false)` o falta de banderas `XMLPARSE_NOENT` desactivadas). 
+ Entorno de Red:** Los puertos e instancias dinámicas de picoCTF (`saturn.picoctf.net` / `atlas.picoctf.net`) requieren actualizar la cabecera `Host` y el puerto asignado en cada sesión.
## Referencias
https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing) * [OWASP - XXE Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Preventative_Cheat_Sheet.html)

