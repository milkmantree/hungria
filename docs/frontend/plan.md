# Plan de frontend (UX/UI)

Estado: **planeado, sin empezar**. El [ADR 0013](../adr/0013-stack-y-arquitectura.md) dejó el frontend pendiente; este documento fija la ruta para decidirlo y construirlo. Regla: primero se decide y luego se construye, y la dirección de diseño va antes que los componentes.

## Herramientas
- **Impeccable** ([pbakaus/impeccable](https://github.com/pbakaus/impeccable)): skill de diseño para Claude Code. Su comando `shape` hace una entrevista de descubrimiento y produce un brief de diseño sin escribir código. También ofrece comandos de crítica y auditoría. Aporta la dirección y la revisión.
- **Astryx** ([meta/astryx](https://github.com/meta/astryx)): sistema de diseño open source de Meta (MIT, en beta) sobre React 19 y StyleX. Trae más de 150 componentes accesibles, siete temas basados en variables CSS, plantillas y una CLI con servidor MCP. Aporta los componentes.
- Ninguna está instalada. Los datos vienen de resúmenes de terceros: confirmar en la documentación oficial, sobre todo los nombres de los comandos de Impeccable.

## Tres interfaces, tres briefs
| Interfaz | Rasgos | Astryx |
|---|---|---|
| PWA del cliente (Mesa digital) | móvil, cálida, español e inglés | se decide tras la prueba |
| App del mesero (Sala) | rápida, densa, usable con una mano | candidato claro |
| Back-office del encargado (Núcleo) | tablas y configuración | candidato claro |

## Pasos
1. **Briefs (sin código).** Ejecutar `shape` una vez por interfaz, partiendo de [visión](../vision.md), [principios](../plataforma/principios.md) y el [prototipo](../prototipo.md), para que solo pregunte tono, referencias y densidad. Guardar cada brief en `docs/frontend/briefs/`, en español. Empezar por la app del mesero, la más acotada.
2. **Prueba de Astryx (en paralelo).** En una carpeta aparte, fuera del repo, con Vite y React 19, construir tres pantallas: la carta del cliente en móvil, la lista de pedidos del mesero y el mapa de mesas. Criterios para seguir:
   - español e inglés funcionan;
   - el peso del bundle en móvil es aceptable;
   - los botones son cómodos al tacto;
   - el tema se puede acercar a lo que pide el brief.

   Si falla para la PWA del cliente, Astryx queda solo para mesero y back-office. Si falla en todo, se descarta.
3. **ADR 0014 (frontend).** Decidir el stack (React con Astryx o no), dónde vive el código (propuesta: `frontend/` en este repo, con su propio `CLAUDE.md`) y el tema base y los tokens que salgan de los briefs.
4. **Construir por flujo (01 a 05).** La CLI y el MCP de Astryx eligen el componente o la plantilla de cada pantalla; Impeccable critica y audita contra el brief; los ajustes de estilo van como variables del tema; `swizzle` (copiar el código de un componente al proyecto) solo cuando haga falta.

## Cuidados
- `npx @astryxdesign/cli init` escribe `AGENTS.md` o `CLAUDE.md`. Ejecutarlo solo dentro de `frontend/` o de la carpeta de prueba, nunca en la raíz: pisaría el `CLAUDE.md` del repo.
- No dejar que dos skills de estilo opinen sobre el mismo código: Impeccable decide el diseño y Astryx pone la API de los componentes. Leer el `SKILL.md` de cada una antes de instalarla.
- Sin verificar de Astryx: soporte de español e inglés, funcionamiento offline y como PWA, y rendimiento en móvil.
- Riesgos: está en beta con versiones que cambian rápido (0.7), depende de un solo proveedor (Meta) y nació para herramientas internas de escritorio, así que la PWA del cliente podría verse genérica.

## Al retomar
Hacer la prueba de Astryx en una carpeta temporal, ejecutar `shape` para la app del mesero y luego escribir el ADR 0014.
