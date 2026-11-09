# Módulo: Mesa digital

Estado: fase 1, diseño. Autoservicio del cliente en la mesa. Requiere Sala; con Pagos habilita el modo Directo ([ADR 0009](../adr/0009-licencias-y-activacion-de-modulos.md)). Documentos del modelo: [sesión de mesa](../sesion-de-mesa.md), [modos de servicio](../modos-de-servicio.md), [acceso a la mesa](../acceso-a-la-mesa.md).

## Responsabilidades
- **PWA del cliente** en español e inglés, sin instalar nada.
- **Acceso a la mesa** por NFC con SDM o por QR; validación del toque.
- **Identidad anónima** con nombre de animal.
- **Grupos autónomos:** crear grupo, vincular invitados de forma explícita, pedir unirse a uno existente.
- **Carta con búsqueda** y armado del pedido del grupo; autodeclaración de edad para alcohol.
- **Modos de servicio:** Directo (pago en la PWA, requiere Pagos) y Acompañado (aviso al mesero).
- **Botón de llamado** al mesero con motivo.
- **Feedback** privado, breve y opcional al cerrar el grupo; alerta al encargado si es negativo e invitación a dejar una reseña en Google si es bueno.

## Requisitos
R1, R2, R3, R4 (búsqueda), R6, R7, R9, R14, R17, R20, R34. Ver [requisitos](requisitos.md).

## Contratos
| Con | Mesa digital envía | Mesa digital recibe |
|---|---|---|
| Sala | pedidos para confirmar (Acompañado), pedidos pagados (Directo), llamados con motivo, solicitudes de unión | estado de la sesión, grupos, pedidos confirmados o editados, expulsiones |
| Pagos y comprobantes | solicitud de cobro del grupo, propina, RUC si pide factura, destino del comprobante | pago confirmado o rechazado, saldo a favor, comprobante emitido |
| Cuenta de cliente (futuro) | identidad opcional del cliente | historial de visitas, comprobantes |
| Núcleo | feedback negativo (para alertas y auditoría) | carta, traducciones y disponibilidad |

Qué hace Mesa digital cuando falta cada módulo opcional: [dependencias](dependencias.md#mesa-digital).
