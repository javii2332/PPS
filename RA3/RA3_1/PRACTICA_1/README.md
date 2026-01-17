# Práctica 1: Hardening de Apache (Base)

### 1. Explicación
En esta capa base, se ha configurado un servidor Apache sobre Debian Bullseye aplicando medidas iniciales de endurecimiento:
- **Ocultación de Servidor:** Se configuró `ServerTokens ProductOnly` y `ServerSignature Off`.
- **Cabeceras de Seguridad:** Implementación de **HSTS** (Strict-Transport-Security) y **CSP** (Content-Security-Policy).
- **Deshabilitación de Autoindex:** Se desactivó el listado de directorios para evitar la exposición de archivos.

### 2. Validación
Para verificar la ocultación de versión y las cabeceras:
`curl -I http://localhost:8080`

### 3. Captura de pantalla
![Validación P1](validación_p1.png)
*(Sube aquí una captura del comando curl donde no se vea la versión de Debian)*

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p1_javlluapa:latest
