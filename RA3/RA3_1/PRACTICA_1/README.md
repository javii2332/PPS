# Práctica 1: Hardening de Apache (Capa Base)

### 1. Explicación
En esta capa base, se ha configurado un servidor Apache sobre **Debian Bullseye** aplicando medidas iniciales de endurecimiento (*hardening*). El objetivo es reducir la superficie de exposición y mejorar la seguridad de las comunicaciones.

**Medidas implementadas:**
* **Ocultación de Servidor:** Se configuró `ServerTokens ProductOnly` y `ServerSignature Off` para evitar que atacantes conozcan la versión exacta del sistema.
* **HSTS (HTTP Strict Transport Security):** Implementación de la cabecera para obligar al navegador a usar HTTPS durante 2 años.
* **CSP (Content-Security-Policy):** Capa de seguridad para prevenir ataques de inyección de datos y XSS.
* **Deshabilitación de Autoindex:** Se desactivó el listado automático de directorios para evitar la exposición accidental de archivos.
* **Seguridad SSL/TLS:** Habilitación del módulo SSL y activación del sitio seguro por defecto con certificados *snakeoil*.

### 2. Guía de Despliegue
Este repositorio utiliza una imagen preconfigurada alojada en Docker Hub. No necesitas los archivos de configuración locales para lanzarlo, ya que el archivo `csp_hsts.conf` y el resto de ajustes están integrados en la imagen.

**Paso 1: Descargar la imagen**
`docker pull javi2332/pps_p1_javlluapa:latest`

**Paso 2: Lanzar el contenedor**
Mapeamos el puerto 8080 para HTTP y el 8081 para HTTPS (puerto 443 interno):

```bash
docker run -d \
  --name harden_base \
  -p 8080:80 \
  -p 8081:443 \
  javi2332/pps_p1_javlluapa:latest
3. Validación y Auditoría
Para verificar que todas las medidas de seguridad se han aplicado correctamente, realizamos peticiones al contenedor:

Verificación de Ocultación y Cabeceras (HTTP) curl -I http://localhost:8080

Verificación de HTTPS y HSTS (Puerto Seguro) Nota: Usamos -k porque los certificados son autofirmados. curl -Ik https://localhost:8081

Resultado esperado: Deberías observar las siguientes cabeceras en la respuesta:

Plaintext

Server: Apache (Sin versiones).
Strict-Transport-Security: max-age=63072000; includeSubDomains
Content-Security-Policy: default-src 'self'; img-src *; ...
4. URL Docker Hub
La imagen oficial de esta práctica se encuentra en: 👉 javi2332/pps_p1_javlluapa

5. Limpieza
Si deseas detener y borrar el contenedor de prueba: docker rm -f harden_base


---

### ¿Qué hemos logrado con este código?
1. **Jerarquía visual:** El título principal usa `#` y los puntos clave usan `###` para que se vean grandes y claros.
2. **Resaltado de comandos:** He usado los acentos graves ( \` ) para los comandos cortos (como el pull o el rm) para que resalten sobre el texto.
3. **Bloques de código:** He usado ` ```bash ` y ` ```text ` para las partes más largas (el comando `run` y el resultado esperado) para que tengan ese fondo oscuro y estilo de terminal que tanto te gusta.

¿Te gustaría que te ayude a revisar también el Dockerfile de la segunda práctica para asegurar que hereda todo esto sin errores?
