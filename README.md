# 📱 WAHA - WhatsApp HTTP API

> Stack de Docker Compose para desplegar [WAHA](https://waha.devlike.pro/) en Portainer.
> Reemplazo de Evolution API.

## 🚀 Despliegue en Portainer (Git Stack)

### 1. Crear el Stack desde Git

1. En Portainer, ir a **Stacks** → **+ Add stack**
2. Seleccionar **Repository**
3. Configurar:
   - **Repository URL**: `https://github.com/elitealma/waha.git`
   - **Repository reference**: `main`
   - **Compose path**: `docker-compose.yml`

### 2. Configurar Variables de Entorno

En la sección **Environment variables** de Portainer, agregar:

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `WAHA_API_KEY` | API Key para autenticación | `a1b2c3d4e5f6...` (UUID largo) |
| `WAHA_DASHBOARD_USERNAME` | Usuario del dashboard | `admin` |
| `WAHA_DASHBOARD_PASSWORD` | Contraseña del dashboard | `password-seguro-aqui` |
| `WHATSAPP_SWAGGER_USERNAME` | Usuario de Swagger | `admin` |
| `WHATSAPP_SWAGGER_PASSWORD` | Contraseña de Swagger | `password-seguro-aqui` |
| `WAHA_BASE_URL` | URL base del servidor | `http://tu-ip:3000` |

### 3. Deploy

Click en **Deploy the stack** y esperar a que el contenedor esté corriendo.

### 4. Acceder

- **Dashboard**: `http://tu-ip:3000/dashboard`
- **Swagger API**: `http://tu-ip:3000/api/docs`

---

## 🔧 Despliegue Manual (Docker Compose)

```bash
# 1. Clonar el repositorio
git clone https://github.com/elitealma/waha.git
cd waha-docker-stack

# 2. Crear el archivo .env desde el template
cp .env.example .env

# 3. Editar con tus credenciales
nano .env

# 4. Levantar el stack
docker compose up -d

# 5. Verificar que está corriendo
docker compose ps
docker compose logs -f
```

---

## 📋 Comandos Útiles

```bash
# Ver logs en tiempo real
docker compose logs -f

# Reiniciar el servicio
docker compose restart

# Detener todo
docker compose down

# Actualizar a última versión
docker compose pull
docker compose up -d
```

---

## 🔗 Integración con n8n

Para conectar WAHA con n8n, configurar las variables de webhook:

```env
WHATSAPP_HOOK_URL=http://tu-n8n:5678/webhook/waha
WHATSAPP_HOOK_EVENTS=message,message.any,state.change
```

O configurar webhooks por instancia desde el Dashboard de WAHA.

---

## 📚 Documentación

- [WAHA Docs](https://waha.devlike.pro/docs/overview/quick-start/)
- [Configuración](https://waha.devlike.pro/docs/how-to/config/)
- [Enviar mensajes](https://waha.devlike.pro/docs/how-to/send-messages/)
- [Recibir mensajes](https://waha.devlike.pro/docs/how-to/receive-messages/)
- [Dashboard](https://waha.devlike.pro/docs/how-to/dashboard/)
- [Seguridad](https://waha.devlike.pro/docs/how-to/security/)

---

## ⚠️ Seguridad

> **¡IMPORTANTE!** Nunca uses contraseñas débiles en producción.
> Los atacantes pueden encontrar tu servidor y abusar de tus sesiones de WhatsApp.

Genera claves seguras con:
```bash
# Linux/Mac
uuidgen | tr -d '-'

# O usa cualquier generador de UUID online
```

---

## 📂 Estructura del Proyecto

```
├── docker-compose.yml    # Stack principal para Portainer
├── .env.example          # Template de variables de entorno
├── .gitignore            # Excluye .env y archivos sensibles
└── README.md             # Esta documentación
```
