# Práctica 4: Protección DoS con Mod_Evasive

### 1. Explicación
Capa final que hereda la seguridad total de la **P3** y añade protección contra denegación de servicio:
- **Estrategia en cascada:** Basado en la imagen `pps_p3_javlluapa`.
- **Mod_Evasive:** Configurado para detectar ataques de fuerza bruta o DoS y bloquear la IP temporalmente.

### 2. Validación
Ejecución del script de prueba de carga:
`docker exec -it <contenedor> perl /root/test.pl`
*(Se debe observar cómo las peticiones pasan de 200 OK a 403 Forbidden)*

### 3. Captura de pantalla
![Validación P4](validación_p4.png)

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p4_javlluapa:latest
