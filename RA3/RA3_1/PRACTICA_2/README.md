# Práctica 2: ModSecurity (WAF Base)

### 1. Explicación
Esta imagen hereda de la **P1** y añade la capa del Firewall de Aplicación Web (WAF):
- **Estrategia en cascada:** Se utiliza la imagen `pps_p1_javlluapa` como base.
- **ModSecurity:** Instalación y activación del motor en modo bloqueo (`SecRuleEngine On`).

### 2. Validación
Comprobación de que el módulo está cargado:
`docker exec <contenedor> apache2ctl -M | grep security`
Comprobación de que el WAF funciona mediante un intento de ataque (Path Traversal):
`curl -I "http://localhost:8080/index.php?exec=/bin/bash"`

### 3. Captura de pantalla
<img width="900" height="142" alt="image" src="https://github.com/user-attachments/assets/39230155-eed3-47e2-981f-b6aee2f7067e" />

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p2_javlluapa:latest
