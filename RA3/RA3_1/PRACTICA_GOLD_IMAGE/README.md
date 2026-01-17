# Práctica Final: Golden Image Apache (Hardening Extremo)

## 1. Introducción

Esta imagen representa la culminación del proyecto de seguridad en servidores web. Se ha diseñado como una **Golden Image**, una imagen de referencia que consolida todas las capas de seguridad configuradas en las prácticas anteriores, sumando protecciones críticas a nivel de sistema operativo, usuario y protocolo.
La imagen sigue una **estrategia de herencia en cascada**, lo que garantiza que este contenedor final sea el más robusto de toda la serie.

## 2. Estructura de Herencia (Cascada)

Para maximizar la eficiencia y el orden, esta imagen se apoya en el trabajo previo siguiendo este árbol de capas:
* **Capa Base:** `debian:bullseye`
* **P1:** Hardening básico y cabeceras de seguridad.
* **P2:** Instalación y activación de ModSecurity (WAF).
* **P3:** Integración de reglas OWASP CRS.
* **P4:** Protección contra DoS con Mod_Evasive.
* **P_Certificados:** Implementación de SSL/TLS (Puerto 443).
* **GOLD_IMAGE (Final):** Hardening de sistema, gestión de usuarios y protocolos.



## 3. Mejoras de Seguridad Implementadas

En esta fase final se han añadido los siguientes controles basados en estándares de endurecimiento (Hardening) industrial:
* **Usuario sin privilegios:** El servicio Apache se ha configurado para ejecutarse bajo el usuario y grupo **apache**. El servicio ya no corre como `root` o `www-data`, minimizando la superficie de ataque.
* **Hardening de Permisos:** Se ha aplicado un `chmod 750` a las carpetas de configuración (`/etc/apache2`) y binarios, impidiendo que usuarios no autorizados lean la configuración.
* **Deshabilitación de HTTP 1.0:** Mediante `mod_rewrite` inyectado, se obliga el uso de HTTP 1.1, mitigando vulnerabilidades de secuestro de sesión asociadas a versiones antiguas.
* **Ocultación de Identidad (Server Banner):** Se han forzado las directivas `ServerTokens Prod` y `ServerSignature Off` para enmascarar totalmente la identidad del servidor.
* **Seguridad de Cookies:** Configuración de banderas `HttpOnly` y `Secure` para mitigar ataques XSS y robo de sesiones.
* **Protección contra Clickjacking:** Implementación de la cabecera `X-Frame-Options: SAMEORIGIN`.
* **Inyección de Configuración Segura:** Las directivas se inyectan directamente en `apache2.conf` para garantizar que los módulos `headers` y `rewrite` estén operativos antes de aplicar las reglas.

## 4. Archivos de Configuración Incluidos

Para el despliegue de esta imagen se utilizan los siguientes archivos incluidos en este directorio:
* **dockerfile:** Define la herencia desde la imagen de certificados, la creación del usuario apache y la inyección de seguridad.
* **default-ssl.conf:** Configuración del VirtualHost seguro y redirección permanente del puerto 80 al 443.

## 5. Validación de la Seguridad

Se han realizado las siguientes pruebas para confirmar la robustez del servidor:

**Verificación de Banner Personalizado:**
`curl -I -k https://localhost:8081`
* **Resultado:** El encabezado "Server" solo muestra "Apache", ocultando la versión y el sistema operativo.

**Verificación de Usuario No Privilegiado:**
`docker exec golden ps -ef | grep apache`
* **Resultado:** Los procesos hijos se ejecutan bajo el usuario **apache**.

**Verificación de Protocolo:**
`curl -I --http1.0 http://localhost:8080`
* **Resultado:** El servidor rechaza o ignora la petición según las reglas de reescritura configuradas.

## 6. Captura de Pantalla

A continuación se muestra la validación mediante `curl` con las cabeceras de seguridad activas:
<img width="940" height="274" alt="image" src="https://github.com/user-attachments/assets/4a216ae2-e97c-4272-9640-29cfcf3be471" />

<img width="709" height="207" alt="image" src="https://github.com/user-attachments/assets/9c1e06fb-ab19-440f-bb64-81c34f115738" />

<img width="955" height="117" alt="image" src="https://github.com/user-attachments/assets/531ba805-dbfc-4ed8-925f-0c0712609b2d" />

<img width="725" height="200" alt="image" src="https://github.com/user-attachments/assets/a79d4a69-673c-47ae-9738-71482046d9c7" />

## 7. URL Docker Hub (Golden Image)

Puedes descargar la imagen final lista para su despliegue con:
`docker pull javi2332/pps_p_gold_image_javlluapa:latest`
