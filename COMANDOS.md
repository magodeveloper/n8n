# Comandos frecuentes - n8n con Docker

## Gestión de contenedores

### Levantar los contenedores (en segundo plano)
```bash
docker compose up -d
```
Inicia todos los servicios (PostgreSQL y n8n) en modo detached (segundo plano).

### Detener los contenedores
```bash
docker compose down
```
Detiene y elimina los contenedores, pero mantiene los datos guardados en los volúmenes.

### Detener los contenedores y eliminar todos los datos
```bash
docker compose down -v
```
Detiene los contenedores y elimina los volúmenes. Se pierden todos los datos (workflows, credenciales, base de datos).

### Reiniciar los contenedores
```bash
docker compose restart
```
Reinicia todos los servicios sin eliminarlos.

### Reiniciar solo n8n (sin tocar PostgreSQL)
```bash
docker compose restart n8n
```
Reinicia únicamente el contenedor de n8n.

---

## Monitoreo

### Ver el estado de los contenedores
```bash
docker compose ps
```
Muestra el estado actual de cada contenedor (running, healthy, exited, etc.).

### Ver los logs en tiempo real
```bash
docker compose logs -f
```
Muestra los logs de todos los servicios y se queda escuchando nuevos mensajes. Presiona `Ctrl+C` para salir.

### Ver los logs solo de n8n
```bash
docker compose logs -f n8n
```
Muestra únicamente los logs del contenedor de n8n en tiempo real.

### Ver los logs solo de PostgreSQL
```bash
docker compose logs -f postgres
```
Muestra únicamente los logs del contenedor de PostgreSQL en tiempo real.

### Ver las últimas 50 líneas de logs
```bash
docker compose logs --tail 50
```
Muestra solo las últimas 50 líneas de logs de todos los servicios.

---

## Actualización

### Actualizar n8n a la última versión
```bash
docker compose pull && docker compose up -d
```
Descarga la imagen más reciente de n8n y reinicia los contenedores con la nueva versión.

### Ver qué versión de n8n está corriendo
```bash
docker compose logs n8n | grep "Version:"
```
Busca en los logs la línea que indica la versión actual de n8n.

---

## Base de datos

### Acceder a la consola de PostgreSQL
```bash
docker exec -it n8n-postgres psql -U n8n -d n8n
```
Abre una sesión interactiva en la base de datos PostgreSQL. Escribe `\q` para salir.

### Crear un backup de la base de datos
```bash
docker exec n8n-postgres pg_dump -U n8n n8n > backup_n8n.sql
```
Exporta toda la base de datos a un archivo SQL en tu carpeta actual.

### Restaurar un backup de la base de datos
```bash
docker exec -i n8n-postgres psql -U n8n -d n8n < backup_n8n.sql
```
Importa un archivo SQL previamente exportado a la base de datos.

---

## Recursos y espacio

### Ver cuánto espacio usan los contenedores
```bash
docker system df
```
Muestra el espacio en disco usado por imágenes, contenedores y volúmenes.

### Limpiar imágenes antiguas no utilizadas
```bash
docker image prune -f
```
Elimina imágenes que ya no están en uso (por ejemplo, versiones anteriores de n8n después de actualizar).

---

## Acceso rápido

| Recurso | URL |
|---|---|
| Editor de n8n | http://localhost:5678 |
| Webhooks de n8n | http://localhost:5678/webhook/ |
| PostgreSQL | localhost:5432 |
