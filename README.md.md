# EasyPark — Kong API Gateway

API Gateway del sistema EasyPark basado en **Kong 3.6** en modo DB-less.

## Arquitectura

```
Frontend (Vercel) → Kong (Railway) → Backend (Railway)
```

## Rutas configuradas

| Ruta | Destino |
|------|---------|
| `/auth/**` | Backend Railway |
| `/parqueaderos/**` | Backend Railway |
| `/reservas/**` | Backend Railway |

## Plugins activos

- **CORS** — permite peticiones desde el frontend en Vercel
- **Rate Limiting** — 120 req/min, 5000 req/hora por IP
- **Response Transformer** — agrega headers de identificación del gateway

## Comportamiento controlado

Si el servicio Kong se detiene, el frontend deja de recibir respuestas del backend de forma inmediata y controlada. El backend sigue funcionando de forma independiente.

## Deploy en Railway

1. Crear nuevo servicio en Railway → Deploy from GitHub
2. Apuntar a este repositorio
3. Railway detecta el `Dockerfile` automáticamente
4. Puerto expuesto: `8000`

## Variables de entorno (Railway)

No se requieren variables de entorno adicionales. La configuración está en `kong.yml`.

## Admin API

El puerto `8001` expone la Admin API de Kong para inspección en tiempo real.
