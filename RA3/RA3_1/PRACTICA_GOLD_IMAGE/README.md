# Práctica Final: Golden Image Apache (Hardening Extremo)

## 1. Introducción
Esta imagen representa la culminación del proyecto de seguridad en servidores web. Se ha diseñado como una **Golden Image**, una imagen de referencia que consolida todas las capas de seguridad configuradas en las prácticas anteriores, sumando protecciones críticas a nivel de sistema operativo, usuario y protocolo.

La imagen sigue una **estrategia de herencia en cascada**, lo que garantiza que este contenedor final sea el más robusto de toda la serie.

---

## 2. Estructura de Herencia (Cascada)
Para maximizar la eficiencia y el orden, esta imagen se apoya en el trabajo previo siguiendo este árbol de capas:

1.  **Capa Base:** `debian:bullseye`
2.  **P1:** Hardening básico y cabeceras de seguridad.
3.  **P2:** Instalación y activación de ModSecurity (WAF).
4.  **P3:** Integración de reglas OWASP CRS.
5.  **P4:** Protección contra DoS con Mod_Evasive.
6.  **P_Certificados:** Implementación de SSL/TLS (Puerto 443).
7.  **GOLD_IMAGE (Final):** Hardening de sistema, gestión de usuarios y protocolos.



---

## 3. Mejoras de Seguridad Implementadas
En esta fase final se han añadido los siguientes controles basados en estándares de endurecimiento (Hardening) industrial:

* **Usuario sin privilegios:** El servicio Apache se ha configurado para ejecutarse bajo el usuario y grupo `apache`. El servicio ya no corre como `root` o `www-data`, minimizando la superficie de ataque.
* **Hardening de Permisos:** Se ha aplicado un `chmod 750` a las carpetas de configuración (`/etc/apache2`) y binarios, impidiendo que usuarios no autorizados lean la configuración.
* **Deshabilitación de HTTP 1.0:** Mediante `mod_rewrite`, se obliga el uso de HTTP 1.1, mitigando vulnerabilidades de secuestro de sesión asociadas a versiones antiguas.
* **Ocultación de Identidad (Server Banner):** Se utiliza la directiva `SecServerSignature` para enmascarar totalmente la identidad del servidor con un nombre personalizado.
* **Seguridad de Cookies:** Configuración de banderas `HttpOnly` y `Secure` para mitigar ataques XSS y robo de sesiones.
* **Protección contra Clickjacking:** Implementación de la cabecera `X-Frame-Options: SAMEORIGIN`.
* **Restricción de Métodos HTTP:** Se han bloqueado los métodos `TRACE`, `PUT` y `DELETE` para evitar fugas de información y manipulaciones externas.

---

## 4. Archivos de Configuración Incluidos
Para el despliegue de esta imagen se utilizan los siguientes archivos incluidos en este directorio:
* `dockerfile`: Define la herencia desde la imagen de certificados y los cambios en el sistema.
* `security-pro.conf`: Bloque consolidado con todas las directivas de seguridad extra.
* `default-ssl.conf`: Configuración del VirtualHost seguro y redirección del puerto 80.

---

## 5. Validación de la Seguridad
Se han realizado las siguientes pruebas para confirmar la robustez del servidor:

1.  **Verificación de Banner Personalizado:**
    ```bash
    curl -I [https://www.midominioseguro.com](https://www.midominioseguro.com)
    ```
    *Resultado: El encabezado "Server" no revela información real del sistema.*

2.  **Verificación de Usuario No Privilegiado:**
    ```bash
    docker exec <ID_CONTENEDOR> ps -ef | grep apache
    ```
    *Resultado: Los procesos hijos se ejecutan bajo el usuario `apache`.*

3.  **Verificación de Protocolo:**
    ```bash
    curl --http1.0 [https://www.midominioseguro.com](https://www.midominioseguro.com)
    ```
    *Resultado: El servidor rechaza la conexión con un error 403 (Forbidden).*

---

## 6. Captura de Pantalla
![Validación Final de Seguridad](validacion_final.png)

---

## 7. URL Docker Hub (Golden Image)
Puedes descargar la imagen final lista para su despliegue con:

```bash
docker pull javi2332/pps_p_gold_image_javlluapa:latest
