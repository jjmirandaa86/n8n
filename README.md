# n8n — Deploy en droplet

Contenedor **n8n** en `app_network`, datos en `/app/n8n`, acceso en **https://n8n.acertijo.dev** (proxy en `ngnix-droplets-sydney`).

## Secrets GitHub

| Secret | Requerido |
|--------|-----------|
| `SSH_KEY` | Sí |
| `SERVER_IP` | Sí |
| `N8N_ENV` | No (`N8N_ENCRYPTION_KEY`, etc.) |

## Contenedor

| Parámetro | Valor |
|-----------|-------|
| Nombre | `n8n` |
| Puerto interno | `5678` |
| Volumen datos | `/app/n8n` → `/home/node/.n8n` |
| Volumen procesed | `/app/projects/uefn-backend/procesed` (workflows UEFN) |

## "Lost connection to the server"

n8n usa **WebSockets** y ejecuciones largas (OpenAI). El proxy nginx debe incluir `Upgrade`, `Connection`, `proxy_read_timeout 3600s` — ver deploy de `ngnix-droplets-sydney`.

Tras cambiar nginx o este deploy: push a `main` en ambos repos y recarga nginx en el servidor.

## Deploy

Push a `main` → `.github/workflows/deploy.yml`
