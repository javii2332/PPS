# Práctica 1: Hardening de Apache (Capa Base)

### 1. Explicación
En esta capa base, se ha configurado un servidor Apache sobre **Debian Bullseye** aplicando medidas iniciales de endurecimiento (*hardening*). El objetivo es reducir la superficie de exposición y mejorar la seguridad de las comunicaciones.

**Medidas implementadas:**
* **Ocultación de Servidor:** Se configuró `ServerTokens ProductOnly` y `ServerSignature Off`.
* **HSTS (HTTP Strict Transport Security):** Implementación de la cabecera para obligar al navegador a usar HTTPS durante 2 años.
* **CSP (Content-Security-Policy):** Capa de seguridad para prevenir ataques de inyección de datos y XSS.
* **Deshabilitación de Autoindex:** Se desactivó el listado automático de directorios.
* **Seguridad SSL/TLS:** Habilitación del módulo SSL y activación de certificados *snakeoil*.

### 2. Guía de Despliegue
Este repositorio utiliza una imagen preconfigurada alojada en Docker Hub. No necesitas los archivos de configuración locales para lanzarlo, ya que el archivo `csp_hsts.conf` y el resto de ajustes están integrados en la imagen.

**Paso 1: Descargar la imagen**

docker pull javi2332/pps_p1_javlluapa:latest

**Paso 2: Lanzar el contenedor**

docker run -d --name harden_base -p 8080:80 -p 8081:443 javi2332/pps_p1_javlluapa:latest

**Paso 3: Validación y Auditoría**

Para verificar que todas las medidas de seguridad se han aplicado correctamente, realizamos peticiones al contenedor:

Verificación de Ocultación y Cabeceras (HTTP y HTTPS)

# Comprobación de cabeceras en puerto 8080
curl -I http://localhost:8080

# Comprobación de puerto seguro (HSTS) en puerto 8081
curl -Ik https://localhost:8081
Resultado esperado:

Plaintext

HTTP/1.1 200 OK
Server: Apache
Strict-Transport-Security: max-age=63072000; includeSubDomains
Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com; script-src 'self';
4. URL Docker Hub
Bash

docker pull javi2332/pps_p1_javlluapa:latest
5. Limpieza
Bash

docker rm -f harden_base
