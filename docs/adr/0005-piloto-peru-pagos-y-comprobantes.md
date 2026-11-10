# ADR 0005 — Piloto en Perú: interfaz, pagos, propinas y comprobantes

- Fecha: 2026-11-05
- Estado: aceptado

## Contexto
Para cerrar el diseño de los flujos hacía falta fijar dónde opera el piloto, cómo se cobra, cómo se emiten los comprobantes y qué pasa con el dinero cuando un pedido pagado cambia.

## Decisión
- **País del piloto:** Perú. Comprobantes electrónicos según SUNAT.
- **Modos de servicio:** el piloto soporta **Directo y Acompañado**, elegibles por configuración del restaurante.
- **Interfaz del cliente:** solo **PWA** (sin app nativa), en **español e inglés** desde el inicio.
- **Medios de pago digitales:** tarjetas de crédito y débito, Yape, Plin, Apple Pay y Google Pay, a través de la pasarela propia de cada restaurante ([ADR 0008](0008-pasarela-propia-de-cada-restaurante.md)). El pago por fuera sigue siempre disponible.
- **Propinas:** se sugiere un **10%** editable al pagar, **por grupo**. También se pueden dejar por fuera.
- **Comprobantes:** se emiten mediante un **PSE/OSE** autorizado por SUNAT. Por defecto es **boleta**; si el cliente quiere **factura**, ingresa su RUC en la PWA al pagar.
- **Cambios sobre pedidos ya pagados (Directo):** el monto queda como **saldo a favor** del grupo en la sesión. Si queda saldo al cerrar, se **reembolsa automáticamente** al medio de pago original.

Detalle: [pagos y comprobantes](../modulos/pagos/pagos-y-comprobantes.md).

## Consecuencias
- Hay que elegir un proveedor PSE/OSE. La pasarela la trae cada restaurante (ADR 0008).
- El saldo a favor evita reembolsos parciales en cada edición, pero exige llevar un saldo por grupo y liquidarlo al cierre.
- La interfaz bilingüe obliga a tener la carta y los textos traducibles desde el inicio.
