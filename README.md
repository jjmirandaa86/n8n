# n8n — Deploy en droplet

Automatización con GitHub Actions: contenedor **n8n** en la red Docker `app_network` y datos persistentes en `/app/n8n`.

El dominio y el proxy (nginx) se configuran en otro proyecto.

## Requisitos

| Requisito         | Detalle                                                                   |
| ----------------- | ------------------------------------------------------------------------- |
| Secrets en GitHub | `SSH_KEY`, `SERVER_IP`                                                    |
| Opcional          | `N8N_ENV` — variables extra (dominio, webhooks, etc.; ver `.env.example`) |

## Contenedor

| Parámetro      | Valor                          |
| -------------- | ------------------------------ |
| Nombre         | `n8n`                          |
| Imagen         | `docker.n8n.io/n8nio/n8n`      |
| Red            | `app_network`                  |
| Volumen host   | `/app/n8n` → `/home/node/.n8n` |
| Puerto interno | `5678`                         |

## Deploy

Push a `main` ejecuta `.github/workflows/deploy.yml`: crea `/app/n8n` y levanta o actualiza el contenedor `n8n`.
