# Práctica 3: Reglas OWASP CRS

### 1. Explicación
Heredando de la **P2**, se integran las reglas oficiales de **OWASP Core Rule Set**:
- **Estrategia en cascada:** Se utiliza la imagen `pps_p2_javlluapa`.
- **Protección Inteligente:** Bloqueo de ataques comunes como SQL Injection y XSS mediante reglas preconfiguradas.

### 2. Validación
Prueba de ataque de Path Traversal bloqueado por OWASP:
`curl -I "http://localhost:8080/?exec=/../../"`
*(Debe devolver un error 403 Forbidden)*

### 3. Captura de pantalla
![Validación P3](validación_p3.png)

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p3_javlluapa:latest
