# Decisiones de arquitectura (ADR)

Cada decisión relevante (elegir una fuente, una dependencia importante, un
cambio de arquitectura) se registra en un archivo corto con este formato:

- Nombre: `NNNN-titulo-corto.md`, numerado correlativamente (`0001-fuente-remotive.md`).
- Un ADR aceptado no se edita: si la decisión cambia, se escribe uno nuevo que
  lo reemplaza y se marca el anterior como "Reemplazado por NNNN".

## Plantilla

```markdown
# NNNN — Título

- Estado: propuesto | aceptado | reemplazado por NNNN
- Fecha: AAAA-MM-DD
- Issue: #N

## Contexto
Qué problema hay y qué restricciones aplican.

## Decisión
Qué se decidió.

## Alternativas descartadas
Qué otras opciones había y por qué no.

## Consecuencias
Qué implica (lo bueno, lo malo, qué hay que vigilar).
```
