# ADR 0012 — Alcance frente a TastyIgniter

- Fecha: 2026-11-09
- Estado: aceptado

## Contexto
Se compararon las funciones de TastyIgniter con las de Hungría ([comparativa](../comparativa-tastyigniter.md)) y se respondió un cuestionario por cada función faltante (F1–F14).

## Decisión
**Carta y precios (Núcleo, fase 1)**
- **Opciones de plato:** opciones obligatorias (elegir una, por ejemplo el punto del lomo) y extras opcionales con precio (F5).
- **Cartas por horario** y horario de atención de cada local (F4).
- **Precios con IGV incluido.** Hungría no maneja recargo al consumo (F11).

**Descuentos (F6)**
- **Cortesías del encargado:** regalar o rehacer un plato sin costo, con motivo y registro en la auditoría. Cubre los errores del local con un ítem ya en preparación.
- **Descuentos manuales del mesero:** porcentaje o monto sobre un ítem o la cuenta, con un límite configurable por local.
- **Cupones y promociones:** módulo extra (códigos, happy hour, 2x1, por local y horario).

**Nuevos canales de venta**
- **Para llevar:** el cliente pide y recoge en el local. Módulo extra (F1).
- **Integración con apps de delivery:** los pedidos de las apps entran directo a Cocina. Módulo extra. Hungría **no** hace delivery propio (F1).
- **Sin sitio web:** los pedidos online se hacen desde un enlace a la PWA que el restaurante publica en su web o redes (F2, F14).

**Reservas (F3)**
- Las **reservas online** entran en la fase 1 dentro de Recepción y reservas, junto con la lista de espera.

**Clientes**
- **Solo feedback privado.** Con buena nota se invita al cliente a dejar una reseña en Google (F7).
- **Cuenta de cliente** (futuro): registro con correo y verificación, login con Google o Apple, tarjeta guardada en la pasarela del restaurante (nunca en Hungría), historial y comprobantes (F8).
- **Notificaciones** por **correo** y **SMS**, con plantillas por tipo de aviso. Es un servicio del Núcleo (F9).

**Plataforma**
- **Reportes avanzados:** módulo extra (F12).
- **Sin API pública** por ahora (F10).
- **Soporte con acceso autorizado:** el restaurante autoriza por tiempo limitado; todo queda en la auditoría y el soporte no ve datos de pago (F13).

## Consecuencias
- La carta del Núcleo crece (opciones, extras, horarios) y la comanda debe llevar las opciones elegidas.
- Aparecen cuatro módulos extra: Para llevar, Delivery por apps, Cupones y promociones, Reportes avanzados.
- La fase 1 incluye diseñar reservas online.
- El SMS tiene costo por mensaje; hay que elegir proveedor.
