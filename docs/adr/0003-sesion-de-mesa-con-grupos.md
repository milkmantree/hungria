# ADR 0003 — Sesión de mesa con grupos

- Fecha: 2026-10-26
- Estado: aceptado

## Contexto
Una mesa suele tener varias personas con distintas formas de pagar: todos juntos, cada uno lo suyo, o subgrupos. Un único titular por mesa no lo cubre.

## Decisión
- La mesa es una **sesión** que contiene uno o más **grupos**. Cada grupo tiene un titular, invitados vinculados, cuenta, pago y comprobantes propios.
- Un comensal solo es un grupo de una persona.
- Vincular invitados es **explícito**; un comensal pertenece a un grupo a la vez.
- Los platos compartidos se cargan a un solo grupo.
- El mesero puede editar cualquier pedido y expulsar participantes.
- La sesión cierra al liquidarse el último grupo.

Detalle: [sesión de mesa](../sesion-de-mesa.md).

## Consecuencias
- Cada comensal puede pagar a su ritmo y salir cuando quiera.
- Más estados que manejar (sesión y grupo) y casos de reasignación a cargo del mesero.
- El modelo no distingue a un comensal solo de un grupo grande, lo que simplifica la lógica.
