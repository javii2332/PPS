# Práctica 3: Reglas OWASP CRS

### 1. Explicación
Heredando de la **P2**, se integran las reglas oficiales de **OWASP Core Rule Set**:
- **Estrategia en cascada:** Se utiliza la imagen `pps_p2_javlluapa`.
- **Protección Inteligente:** Bloqueo de ataques comunes como SQL Injection y XSS mediante reglas preconfiguradas.

### 2. Validación
Prueba de ataque de Path Traversal bloqueado por OWASP:
`curl -I "http://localhost:8080/?exec=/../../"`
*(Debe devolver un error 403 Forbidden)*

Visualización de logs, ataque detectado por el servidor y cazado por las reglas OWASP:
`docker exec "contenedor" tail -f /var/log/apache2/error.log`

### 3. Captura de pantalla
<img width="906" height="287" alt="image" src="https://github.com/user-attachments/assets/5f3eab75-d4b2-4803-a0e3-529fcff8d3fd" />

<img width="910" height="585" alt="image" src="https://github.com/user-attachments/assets/82f7c287-5524-41f4-8f77-b728c86ea863" />

<img width="910" height="48" alt="image" src="https://github.com/user-attachments/assets/94b538ab-e934-4477-ab4f-513885a244d8" />

<img width="896" height="48" alt="image" src="https://github.com/user-attachments/assets/e074c6ca-5815-4639-a9f8-a6cf12bb4d49" />

<img width="896" height="67" alt="image" src="https://github.com/user-attachments/assets/7eeaabc8-3d8e-4ab9-9d51-8a2357f4f19f" />

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p3_javlluapa:latest
