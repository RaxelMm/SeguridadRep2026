# Descripcion
How about we take you on an adventure on exploring certificate signing requests Take a look at this CSR file [here](https://challenge-files.cylabacademy.net/library/5106e781bbd36dcc1335e6ad005b28467f171c07351768e71d06bf9cafb3c1f6/readmycert.csr).
## Solución

El reto "ReadMyCert" nos proporciona un archivo CSR (*Certificate Signing Request*) en formato PEM llamado `readmycert.csr`. La pista nos invita a descargar la solicitud de certificado y leer su contenido.

1. **¿Qué es un CSR?**:

   - Una Solicitud de Firma de Certificado contiene información de identidad (como el nombre de dominio, organización y país) empaquetada junto con la clave pública del solicitante en formato ASN.1 / PKCS#10 codificado en Base64.

2. **Lectura e inspección del CSR**:

   - Al inspeccionar los atributos del sujeto (*Subject*) del certificado (usando OpenSSL o la biblioteca `cryptography` de Python), encontramos que la bandera se encuentra configurada en el campo **Common Name (CN)**:

     ```text

     CN = academy{read_mycert_52274715}

     ```

Bandera obtenida: `academy{read_mycert_52274715}`

## Notas Adicionales

- **Resolución con OpenSSL (Linux / Bash)**:

  - Para inspeccionar todos los detalles del CSR:

    ```bash

    openssl req -in readmycert.csr -noout -text

    ```

  - Para extraer únicamente la línea del sujeto:

    ```bash

    openssl req -in readmycert.csr -noout -subject

    ```

- **Resolución con Python**:

  `python`

  `from cryptography import x509`

  `from cryptography.hazmat.backends import default_backend`

  `with open("readmycert.csr", "rb") as f:`

      `csr = x509.load_pem_x509_csr(f.read(), default_backend())`

  `for attribute in csr.subject:`

      `if attribute.oid == x509.NameOID.COMMON_NAME:`

          `print("Bandera:", attribute.value)`

- **Visor online**: Al ser un archivo en formato estándar PEM, también se puede copiar y pegar el texto en herramientas web como el decodificador de certificados de SSLShopper (_CSR Decoder_).

## Referencias

- [RFC 2986 - PKCS #10: Certification Request Syntax Specification](https://datatracker.ietf.org/doc/html/rfc2986)
- [OpenSSL Documentation - req command](https://docs.openssl.org/master/man1/openssl-req/)
- [Python Cryptography Library - X.509 CSRs](https://cryptography.io/en/latest/x509/reference/#certificate-signing-requests-csrs)

