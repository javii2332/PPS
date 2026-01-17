# Práctica 2: ModSecurity (WAF Base)

### 1. Explicación
Esta imagen hereda de la **P1** y añade la capa del Firewall de Aplicación Web (WAF):
- **Estrategia en cascada:** Se utiliza la imagen `pps_p1_javlluapa` como base.
- **ModSecurity:** Instalación y activación del motor en modo bloqueo (`SecRuleEngine On`).

### 2. Validación
Comprobación de que el módulo está cargado:
`docker exec <contenedor> apache2ctl -M | grep security`

### 3. Captura de pantalla
![Validación P2](validación_p2.png)

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p2_javlluapa:latest
