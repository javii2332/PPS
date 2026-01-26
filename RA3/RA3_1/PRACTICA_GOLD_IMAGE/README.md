# Práctica Final: Golden Image Apache (Hardening Nivel Industrial)

## 1. Introducción
Esta imagen representa la culminación del proyecto de seguridad en servidores web. Se ha diseñado como una **Golden Image**, una imagen de referencia que consolida todas las capas de seguridad configuradas en las prácticas anteriores, sumando protecciones críticas a nivel de sistema operativo, usuario y protocolo.

La imagen sigue una **estratia de herencia en cascada**, garantizando que este contenedor final sea el más robusto de toda la serie:
* **P1 a P4:** Hardening básico, WAF (ModSecurity), Reglas OWASP y protección Anti-DoS (Mod_Evasive).
* **P5:** Cifrado SSL/TLS y activación real de la política **HSTS**.
* **GOLDEN IMAGE (Final):** Hardening de sistema, gestión de usuarios y blindaje de protocolos.

## 2. Justificación Técnica de la Implementación

Para esta fase final, se ha optado por un enfoque de **"Cirugía y Modularidad"** en lugar de sustitución completa:

### A. Uso de Archivo de Configuración Externo (`a2enconf`)
En lugar de inyectar decenas de líneas mediante comandos `echo` en el archivo principal, se ha creado el archivo `gold-image-hardening.conf`. 
* **Razón:** Esto permite mantener la herencia de las prácticas anteriores intacta. Al usar `a2enconf`, Apache carga estas nuevas reglas de seguridad de forma modular, permitiendo una auditoría más clara y evitando errores de sintaxis en el archivo maestro `apache2.conf`.

### B. Uso de `sed` para Variables de Envorno
Se ha utilizado el comando `sed` exclusivamente para modificar el archivo `/etc/apache2/envvars`.
* **Razón:** En distribuciones basadas en Debian, el usuario que ejecuta Apache se define en este archivo. El uso de `sed` es la forma más eficiente de realizar este cambio de identidad de forma persistente sin tener que sobrescribir el archivo completo del sistema.



## 3. El Archivo Externo: `gold-image-hardening.conf`
Este archivo actúa como el "escudo final" del servidor. Su función es centralizar las directivas de seguridad avanzada que no se cubrieron en fases previas:

* **Hardening de Protocolo:** Incluye `TraceEnable Off` y `FileETag None` para evitar ataques de Cross-Site Tracing y fugas de información del inodo del sistema.
* **Gestión de Timeouts:** Reduce el `Timeout` a 60 segundos para mitigar ataques de denegación de servicio de conexión lenta (Slow Loris).
* **Blindaje de Directorios y Métodos:** * Desactiva el listado de directorios (`-Indexes`) y las inclusiones del lado del servidor (`-Includes`).
    * Implementa `<LimitExcept>`, que actúa como una lista blanca permitiendo solo los métodos `GET`, `POST` y `HEAD`, denegando cualquier otro intento (como `PUT` o `DELETE`).
* **Forzado de HTTP 1.1:** Utiliza el motor de reescritura para rechazar peticiones que utilicen el protocolo HTTP 1.0, eliminando riesgos de seguridad heredados.
* **Seguridad de Capa de Aplicación:** Define las cabeceras `X-Frame-Options` y `X-XSS-Protection` para proteger al cliente final.

## 4. Mejoras de Seguridad Implementadas (Capa Final)
* **Usuario sin privilegios:** El servicio Apache se ejecuta bajo el usuario **apache**, aislándolo de `root`.
* **Hardening de Permisos:** Aplicación de permisos restrictivos (`750`) en directorios de configuración.
* **Ocultación de Identidad:** Forzado de `ServerTokens Prod` para enmascarar la infraestructura.

## 5. Validación de la Seguridad (Evidencias)

### A. Verificación de Identidad y Cabeceras Globales
**Comando:** `curl -I -k https://www.midominioseguro.com:8081`

> [!IMPORTANT]
> **Captura de evidencia (Cabeceras):**
> ![Evidencia Curl Headers](https://github.com/user-attachments/assets/2d00f5a6-8e10-4db6-bf8f-aacbe4e11e94)

### B. Verificación de Usuario No Privilegiado
**Comando:** `docker exec pps_gold_javlluapa ps -ef | grep apache`

> [!IMPORTANT]
> **Captura de evidencia (Procesos):**
> ![Evidencia ps -ef](https://github.com/user-attachments/assets/ae9bbfeb-e68a-439a-8e9e-31db8bbe6fac)



### C. Persistencia de la Herencia (WAF y SSL)
**Comando (Simulación de ataque):**
`curl -I -k "https://www.midominioseguro.com:8081/?exec=/bin/bash"`
**Resultado:** `403 Forbidden` (Bloqueado por ModSecurity).

## 6. URL Docker Hub (Golden Image)
`docker pull javi2332/pps_gold_javlluapa:latest`

## 7. Conclusión
Este proyecto demuestra una arquitectura de **Defensa en Profundidad** real. Cada práctica ha añadido una capa de blindaje que la Golden Image final ha consolidado, resultando en un servidor Apache optimizado para resistir ataques modernos.
