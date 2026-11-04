# vigilante-ofertas

Monorepo para aprender a desarrollar con agentes: recolecta ofertas de empleo IT
de una fuente pública, las normaliza y deduplica, y permite seguir el estado de
cada candidatura (nueva → vista → aplicada → entrevista → descartada).

El código lo implementa un agente (Claude Code) y una persona lo supervisa como
jefe técnico: todo cambio entra por rama + PR, y el merge lo hace siempre una
persona.

## Arquitectura

```
frontend (React + Vite + TS, nginx)
        │  HTTP
        ▼
panel (API Laravel + Postgres)      ← seguimiento de candidaturas
        │  HTTP (red interna de Docker)
        ▼
worker (FastAPI + SQLite)           ← scraping, normalización, deduplicación
```

- El frontend **nunca** llama al worker directamente.
- Cada servicio tiene su Dockerfile y su job de CI; `docker-compose.yml` en la
  raíz los une.

| Carpeta | Servicio | Estado |
|---|---|---|
| `worker/` | FastAPI: scraping y `GET /offers` | Fase 1 |
| [`panel/`](panel/) | Laravel (API) + Postgres | Fase 2 |
| [`frontend/`](frontend/) | React + Vite + TypeScript | Fase 3 |

## Fases

0. Setup del repo, guardas del agente y CI.
1. Worker con una fuente (Remotive), tests y Docker.
2. Panel Laravel + Postgres (Pest en CI contra Postgres real).
3. Frontend React + tests E2E con Playwright.
4. Despliegue.

El trabajo está planificado en los
[issues](https://github.com/danessi/vigilante-ofertas/issues) del repo.

## Cómo correrlo

Todavía no hay servicios ejecutables. Las instrucciones de cada servicio se
agregan en su carpeta a medida que se implementan (el worker, en la Fase 1).

## Reglas del proyecto

- Las reglas para agentes están en [`CLAUDE.md`](CLAUDE.md).
- Las decisiones de arquitectura se registran en
  [`docs/decisiones/`](docs/decisiones/).
- Nunca se commitean secretos, datos scrapeados ni archivos personales.

## Licencia

[MIT](LICENSE)
