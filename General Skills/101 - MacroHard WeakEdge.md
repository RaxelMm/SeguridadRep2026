# Descripcion
I've hidden a flag in this file. Can you find it? [Forensics_is_fun.pptm]

## Solucion
1. Los archivos `.pptm` de Office son archivos ZIP. Renombrar el archivo a `.zip`:
   cmd
   copy Forensics_is_fun.pptm Forensics_is_fun.zip

2. Extraer el ZIP con 7-Zip, WinRAR o el explorador de Windows.
    
3. Navegar a la carpeta `ppt/slideMasters/`.
    
4. Abrir el archivo llamado `hidden` con Notepad o VS Code.
    
5. Contiene una cadena en Base64:
    
    text
    
    Z m x h Z z o g Y W N h Z G V t e X t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
    
    (Sin espacios: `ZmxhZzogYWNhZGVteXtEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ==`)
    Decodificar la cadena Base64:

powershell

[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("ZmxhZzogYWNhZGVteXtEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ==
## Notas Adicionales
- **Vulnerabilidad**: Información oculta en archivos de Office (esteganografía).
    
- Los formatos modernos de Office (`.docx`, `.xlsx`, `.pptx`, `.pptm`) son archivos ZIP.
    
- El archivo `hidden` no tiene extensión y no es visible desde la interfaz de PowerPoint.
    
- Se puede inspeccionar el contenido del ZIP sin extraerlo con:
## Referencias

