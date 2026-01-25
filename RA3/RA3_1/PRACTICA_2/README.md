# Práctica 2: ModSecurity (WAF Base)

### 1. Explicación
Esta imagen hereda de la **P1 (Hardening Base)** y añade una capa de defensa activa mediante un **WAF (Web Application Firewall)**:

* **Estrategia en cascada:** Se utiliza la imagen `javi2332/pps_p1_javlluapa` como base, manteniendo CSP, HSTS y SSL.
* **ModSecurity:** Instalación y activación del motor en modo bloqueo (`SecRuleEngine On`).
* **Protección Activa:** El servidor ahora es capaz de interceptar peticiones maliciosas antes de que lleguen a la aplicación.

### 2. Guía de Despliegue
Este repositorio utiliza una imagen preconfigurada alojada en Docker Hub. Al heredar de la P1, los ajustes de endurecimiento y el firewall ya están integrados en la imagen.

**Paso 1: Descargar la imagen**

`docker pull javi2332/pps_p2_javlluapa:latest`

**Paso 2: Lanzar el contenedor**
Mapeamos el puerto 8080 para HTTP y el 8081 para HTTPS (puerto 443 interno):

`docker run -d --name pps_p2_waf -p 8080:80 -p 8081:443 javi2332/pps_p2_javlluapa:latest`

### 3. Validación y Auditoría

Para verificar que el WAF está operativo y bloqueando amenazas, realizamos una prueba de ataque simulado:

**Comprobación de bloqueo (Path Traversal)**

`curl -I "http://localhost:8080/index.php?exec=/bin/bash"`

Resultado esperado:
*(Aquí pegas tu captura del 403 Forbidden)*
<img width="1083" height="280" alt="image" src="TU_URL_DE_GITHUB_AQUI" />

**Verificación de que el módulo está cargado**

`docker exec pps_p2_waf apache2ctl -M | grep security`

Resultado esperado:
*(Aquí pegas tu captura donde sale security2_module)*
<img width="1083" height="150" alt="image" src="TU_URL_DE_GITHUB_AQUI" />

### 4. URL Docker Hub
`docker pull javi2332/pps_p2_javlluapa:latest`

### 5. Limpieza
Para detener y borrar el contenedor de prueba ejecutamos:

`docker stop pps_p2_waf`

`docker rm -f pps_p2_waf`

Resultado esperado:
<img width="492" height="95" alt="image" src="TU_URL_DE_GITHUB_AQUI" />
