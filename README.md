# 🧩 docker-arcane
**Panel Arcane con Docker Compose**

Este repositorio contiene la configuración de **Docker Compose** para desplegar **Arcane**, una interfaz web moderna y potente para la gestión visual de contenedores Docker, similar a Portainer o Homarr, pero con un enfoque más ligero y personalizable.

---

## ✨ Características de Arcane
- **Panel de control visual:** Gestiona contenedores, imágenes, volúmenes y redes Docker desde una interfaz web intuitiva.  
- **Monitorización en tiempo real:** Visualiza el estado y los recursos consumidos por tus contenedores.  
- **Gestión de volúmenes y logs:** Acceso directo a los registros y configuraciones.  
- **Seguridad integrada:** Claves de cifrado y autenticación mediante JWT.  
- **Despliegue rápido y portable:** Basado en un solo contenedor con persistencia de datos.  

---

## 🚀 Instalación y Despliegue Rápido

### 1. Prerrequisitos
Asegúrate de tener instalados:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

### 2. Archivo de Configuración (`docker-compose.yml`)
Crea o copia el siguiente contenido:

```yaml
# Arcane Docker Compose Configuration
# Generated at 12/10/2025, 14:43:28

services:
  arcane:
    image: ghcr.io/ofkm/arcane:latest
    container_name: arcane
    restart: unless-stopped
    ports:
      - 3552:3552
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - arcane-data:/app/data
    environment:
      - PUID=1000
      - PGID=1000
      - APP_URL=http://localhost:3552
      - ENCRYPTION_KEY=ffa0d78a9290ba119fd4551c511d73bb5391a0321a46aee8b15f29e71313a69b
      - JWT_SECRET=528230f3cd06ef0bee8f151842c158167e003a96303bf4f90a96e668cbc66330
      - DATABASE_URL=file:data/arcane.db?_pragma=journal_mode(WAL)&_pragma=busy_timeout(2500)&_txlock=immediate

volumes:
  arcane-data:
    driver: local
```

---

### 3. Despliegue del Contenedor
Ejecuta:

```bash
docker compose up -d
```

Verifica su estado:

```bash
docker ps
```

---

## 🌐 Acceso al Panel
Abre tu navegador en:

```
http://<DIRECCION_IP_DE_TU_SERVIDOR>:3552
```

Desde allí podrás gestionar contenedores, imágenes y redes de Docker.

---

## ⚙️ Persistencia de Datos
Arcane almacena su configuración y base de datos local en:

```
arcane-data:/app/data
```

Esto garantiza que tu información se mantenga incluso tras reinicios o actualizaciones.

---

## 🔒 Seguridad
Arcane utiliza variables de entorno para manejar claves sensibles:

| Variable | Descripción |
|-----------|--------------|
| `ENCRYPTION_KEY` | Cifra datos internos de la aplicación. |
| `JWT_SECRET` | Firma los tokens de sesión (JWT). |
| `DATABASE_URL` | Ubicación y configuración de la base de datos. |

🧠 **Consejo:** Genera tus propias claves seguras con:

```bash
openssl rand -hex 32
```

Guárdalas en tu archivo `.env` y **no las compartas públicamente**.

---

## 🧰 Mantenimiento y Logs
Ver logs:

```bash
docker logs -f arcane
```

Reiniciar:

```bash
docker restart arcane
```

Actualizar a la última versión:

```bash
docker compose pull && docker compose up -d
```

---

## 📚 Recursos Útiles
- 🌍 Sitio oficial: [https://arcane.ofkm.dev](https://arcane.ofkm.dev)  
- 📘 Repositorio GitHub: [https://github.com/ofkm/arcane](https://github.com/ofkm/arcane)
