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
<img width="906" height="204" alt="image" src="https://github.com/user-attachments/assets/4538ef40-d8a7-4e1b-bf2a-3789cba9ff17" />

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p1_javlluapa:latest
