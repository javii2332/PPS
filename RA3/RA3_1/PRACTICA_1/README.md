Práctica 1: Hardening de Apache (Base)
1. Explicación
En esta capa base, se ha configurado un servidor Apache sobre Debian Bullseye aplicando medidas iniciales de endurecimiento (hardening):

Ocultación de Servidor: Se configuró ServerTokens ProductOnly y ServerSignature Off.

Cabeceras de Seguridad: Implementación de HSTS (Strict-Transport-Security) y CSP (Content-Security-Policy).

Deshabilitación de Autoindex: Se desactivó el listado de directorios para evitar la exposición de archivos.

2. Validación
Comprobación de que las cabeceras de seguridad y la ocultación de versión están activas: curl -I http://localhost:8080

Comprobación de la conexión segura y persistencia HSTS: curl -Ik https://localhost:8081

3. Procedimiento de despliegue
Para lanzar el contenedor con la configuración de seguridad integrada, ejecute los siguientes comandos:

Descarga de la imagen: docker pull javi2332/pps_p1_javlluapa:latest

Ejecución del contenedor: docker run -d --name harden_base -p 8080:80 -p 8081:443 javi2332/pps_p1_javlluapa:latest

4. Captura de pantalla
(Aquí debes pegar tu imagen del terminal donde se vea el resultado del curl que me pasaste antes)

5. URL Docker Hub
Bash

docker pull javi2332/pps_p1_javlluapa:latest
