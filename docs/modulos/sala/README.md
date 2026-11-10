# Módulo: Sala

Estado: fase 1, diseño. Operación del mesero. Siempre se activa junto con Cocina ([ADR 0009](../../adr/0009-licencias-y-activacion-de-modulos.md)). Modelo central: [sesión de mesa](sesion-de-mesa.md).

## Responsabilidades
- Abrir, fusionar, dividir y cerrar la **sesión de mesa**; cierre automático por inactividad.
- Crear y gestionar **grupos**: sin Mesa digital los crea el mesero; con Mesa digital los crean los clientes y el mesero puede corregirlos.
- **Toma de pedidos** por el mesero en su dispositivo; revisión humana de alergias y notas.
- **Confirmar pedidos** en modo Acompañado, cuando vienen de Mesa digital.
- Editar pedidos, mover ítems entre grupos, reasignar platos compartidos y expulsar participantes.
- Recibir **llamados** y alertas (a todos los meseros del local, o por zona si está Personal).
- Llevar la **cuenta** de cada grupo y registrar **pagos por fuera**.
- **Descuentos del mesero** (con límite por local) y **cortesías del encargado**, con motivo.
- Enviar cada **cuenta cerrada al sistema de caja** del restaurante.

## Requisitos
R2, R5, R7, R8, R9, R10, R11, R13, R21, R24, R25, R26, R31. Ver [requisitos](../../plataforma/requisitos.md).

## Contratos
| Con | Sala envía | Sala recibe |
|---|---|---|
| Cocina | comanda (ítems, notas, alergias, mesa, grupo) | estado por plato (recibido, en preparación, listo) |
| Mesa digital | estado de la sesión, grupos, pedidos confirmados, edición del mesero | pedidos para confirmar, pedidos pagados (Directo), llamados con motivo |
| Pagos y comprobantes | cargo por grupo, pagos por fuera, ajustes que generan saldo a favor | pago confirmado, saldo del grupo, comprobante emitido |
| Personal | llamados y alertas por mesa o zona | asignación de mesas y zonas por turno |
| Inventario | consumo por ítem vendido | disponibilidad de la carta (vía Núcleo) |
| Recepción y reservas | mesa liberada o por liberarse | grupo asignado a una mesa |
| Sistema de caja externo | cuenta cerrada (ítems, montos, propina, medio de pago, comprobante si lo hay) | confirmación de recepción |

Qué hace Sala cuando falta cada módulo opcional: [dependencias](../../plataforma/dependencias.md#sala).
