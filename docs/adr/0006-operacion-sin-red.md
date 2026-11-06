# ADR 0006 — Operación sin red: respaldo en papel y 4G

- Fecha: 2026-11-05
- Estado: aceptado

## Contexto
Hay dos tipos de caída:
- **Cae el internet del local, el servidor sigue arriba.** Los clientes siguen con sus datos móviles; pierden conexión el dispositivo del mesero, la pantalla de cocina y la impresora.
- **Cae el servidor.** Nada digital funciona para nadie.

Se evaluó una cola local en el dispositivo del mesero. Exige una app del mesero que funcione sin conexión, reglas para resolver conflictos entre lo que pide el cliente con datos móviles y lo que edita el mesero, y un servidor dentro del local para que la cocina reciba comandas. Aun así, sin red no hay cobro digital ni validación NFC. Protege poco más que el papel, a un costo mucho mayor.

## Decisión
- **Router con chip 4G de respaldo** en el local para el dispositivo del mesero, la cocina y la impresora.
- Si aun así no hay sistema: **comanda en papel y cobro manual** (efectivo o POS externo).
- Al volver la red, el mesero **registra** lo hecho en papel (pedidos y pagos) y el sistema reconcilia.
- El registro posterior se define como un contrato explícito, para poder sumar una cola local más adelante sin rediseñar.

## Consecuencias
- Costo bajo: un router 4G y un plan de datos.
- Durante la caída del servidor no hay modo Directo ni acceso por NFC; todo pasa por el mesero.
- Los comprobantes digitales se emiten al reconectar.
