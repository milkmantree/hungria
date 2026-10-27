# ADR 0001 — Arquitectura modular con contratos

- Fecha: 2026-10-26
- Estado: aceptado

## Contexto
Hungría cubrirá muchas áreas (atención al cliente, cocina, personal, inventario, ...). Se construirán en el tiempo y un restaurante podría adoptar solo algunas.

## Decisión
Cada área es un **módulo independiente** que se comunica con otros mediante **contratos explícitos** (eventos y datos documentados), nunca accediendo a internos ajenos. Los contratos se documentan en `docs/modulos/` antes de implementarse.

## Consecuencias
- Un módulo puede adoptarse, sustituirse o evolucionar sin romper a los demás.
- Hay costo inicial de definir contratos; se compensa con menos acoplamiento.
- Un módulo ausente no debe impedir que otro funcione (degradación elegante).
- Los flujos de fase 1 identifican los contratos que atención al cliente necesitará de cocina, inventario y personal.
