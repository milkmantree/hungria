# ADR 0002 — Repo como fuente de verdad de la documentación

- Fecha: 2026-10-26
- Estado: aceptado

## Contexto
La documentación se mantiene en dos lugares: este repo y el second brain (`~/brain/hungria/`).

## Decisión
- **Repo (`docs/`)**: fuente de verdad del producto: visión, principios, flujos, módulos, ADRs, glosario.
- **Brain**: solo decisiones destiladas, gotchas y contexto de sesión, con punteros al repo. No se duplican las specs.
- El brain es dual-register (`AI/` + `human/`); el repo está en español, único registro.
- Sin secretos en ninguno de los dos.

## Consecuencias
- Si hay conflicto, gana el repo y se corrige la nota del brain.
- Cambios de flujos o módulos se hacen en el repo; el brain se actualiza solo si cambia una decisión o aparece un gotcha.

## Hospedaje del repo
- 2026-10-26: el repo se aloja en GitHub como **público** (`milkmantree/hungria`), de forma temporal, porque trabajan dos personas y no se quiere pagar por un repo privado.
- Más adelante se migrará a un Forgejo propio; entonces el repo público se hará privado o se eliminará.
- Al ser público, **nunca** se versionan secretos, claves NFC ni datos personales.
