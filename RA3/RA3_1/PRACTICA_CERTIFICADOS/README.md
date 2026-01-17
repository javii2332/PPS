# Práctica: Instalación de Certificado Digital SSL/TLS en Apache

### 1. Explicación
En esta práctica se ha configurado la capa de transporte seguro (SSL/TLS) en Apache mediante la creación de un certificado auto-firmado. Los pasos principales realizados han sido:
- **Generación de Claves:** Creación de una clave privada RSA de 2048 bits y un certificado X.509 válido por 365 días.
- **Automatización:** Uso del parámetro `-subj` en OpenSSL para generar el certificado sin intervención manual durante la construcción de la imagen.
- **Configuración de VirtualHost:** Edición de `default-ssl.conf` para apuntar a los nuevos archivos de certificado (`apache.crt`) y clave (`apache.key`).
- **Redirección Forzosa:** Configuración de una redirección permanente (HTTP 301) del puerto 80 al 443 para asegurar que todo el tráfico sea cifrado.

### 2. Validación
Para validar el funcionamiento, se debe mapear el dominio local en el archivo `/etc/hosts` de la máquina anfitriona:
`127.0.0.1 www.midominioseguro.com`

Al acceder a `https://www.midominioseguro.com`, el navegador mostrará un aviso de seguridad. Esto confirma que:
1. El servidor responde por el puerto **443 (HTTPS)**.
2. El certificado es reconocido aunque no sea de confianza (auto-firmado).
3. Al inspeccionar el certificado, se pueden ver los detalles de la organización (Caminas Web, Castellón, etc.).

### 3. Captura de pantalla
![Aviso de Seguridad y Certificado]
<img width="770" height="731" alt="image" src="https://github.com/user-attachments/assets/26b08c99-c3dd-4ca7-a5fe-32a87cb2fd72" />

<img width="770" height="898" alt="image" src="https://github.com/user-attachments/assets/96770fd3-cda2-465f-ba52-115514de27a4" />

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p_certificados_javlluapa:latest
