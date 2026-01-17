# Práctica 4: Protección DoS con Mod_Evasive

### 1. Explicación
Capa final que hereda la seguridad total de la **P3** y añade protección contra denegación de servicio:
- **Estrategia en cascada:** Basado en la imagen `pps_p3_javlluapa`.
- **Mod_Evasive:** Configurado para detectar ataques de fuerza bruta o DoS y bloquear la IP temporalmente.

### 2. Validación
Ejecución del script de prueba de carga:
`docker exec -it <contenedor> perl /root/test.pl`
*(Se debe observar cómo las peticiones pasan de 200 OK a 403 Forbidden)*

Ejecución de prueba con Apache Bench
`ab -n 100 -c 5 http://localhost:8080/index.html`
*(Se debe observar la cantidad de Failed Requests y Non-2xx responses)*

### 3. Captura de pantalla
<img width="616" height="669" alt="image" src="https://github.com/user-attachments/assets/feb5262a-e9b2-42ed-91e5-8253fc8197e5" />

<img width="762" height="906" alt="image" src="https://github.com/user-attachments/assets/90612c03-aba3-4f7a-9162-6616f755d3cd" />

### 4. URL Docker Hub
```bash
docker pull javi2332/pps_p4_javlluapa:latest
