# Pagos y comprobantes

Decisiones del piloto en Perú: [ADR 0005](adr/0005-piloto-peru-pagos-y-comprobantes.md).

## Pago por grupo
Cada grupo tiene su propia cuenta y paga por separado. El titular paga por sus invitados vinculados. Un plato compartido se carga a un solo grupo (un único pago).

| | Directo | Acompañado |
|---|---|---|
| Cuándo | Al confirmar cada pedido o adición | Al final de la visita del grupo |
| Medios | Digital en la PWA | Digital en la PWA, o con el mesero |
| Efecto | El pago confirma el pedido y lo envía a cocina | El mesero ya confirmó el pedido antes; el pago cierra la cuenta |

## Medios de pago digitales
Cada restaurante conecta **su propia cuenta con API** en una pasarela que opere en Perú; el dinero va directo a esa cuenta ([ADR 0008](adr/0008-pasarela-propia-de-cada-restaurante.md)). La PWA muestra los medios que esa pasarela soporte, entre:
- Tarjetas de crédito y débito.
- Yape y Plin.
- Apple Pay y Google Pay.

Sin pasarela, el restaurante solo puede usar el modo Acompañado con pago por fuera.

## Propina
Al pagar, cada grupo ve una propina sugerida del **10%**, editable y que puede llevar a cero. El restaurante puede cambiar el porcentaje sugerido. La propina también se puede dejar por fuera (efectivo o POS). En Directo se ofrece al cerrar el grupo, no en cada pedido.

## Pago por fuera
Siempre disponible, sin importar el modo original:
1. El cliente llama al mesero desde la sesión.
2. Pagan por un medio externo (POS, efectivo, otro).
3. El mesero **registra en el sistema qué quedó pagado**.
4. Desde ahí el grupo se comporta como en modo Acompañado.

## Adiciones
El cliente puede añadir comida cuando quiera. Genera un nuevo flujo de pago en Directo, o se suma a la cuenta en Acompañado.

## Saldo a favor y reembolsos
Si el mesero cancela o edita un pedido ya pagado (Directo):
1. La diferencia queda como **saldo a favor** del grupo dentro de la sesión.
2. El saldo se descuenta automáticamente de los siguientes pedidos o adiciones del grupo.
3. Si queda saldo al cerrar el grupo, se **reembolsa automáticamente** al medio de pago original.

El mesero indica el motivo de cada cancelación o edición.

## Comprobantes (SUNAT)
Al liquidarse un grupo se emite su comprobante electrónico mediante un **PSE/OSE** autorizado:
- **Boleta** por defecto.
- **Factura** si el cliente ingresa su RUC en la PWA al pagar; se valida la razón social.

El destino lo elige el cliente:
- Su **cuenta en la app**, si está inscrito.
- Su **correo**.
- **Físico**, si lo indica.

Un comprobante por grupo, no por mesa. Cuando se liquida el último grupo, se cierra la sesión ([sesión de mesa](sesion-de-mesa.md)).

## Cobro sin Mesa digital
Si el local tiene Pagos pero no Mesa digital, el mesero genera desde su dispositivo un **QR o link de pago** para el grupo y el cliente paga con su celular. Ver [dependencias](modulos/dependencias.md).

## Envío al sistema de caja
Lo hace el módulo **Sala**, con o sin Pagos: cada cuenta cerrada se envía al sistema de caja del restaurante ([ADR 0007](adr/0007-ventas-al-sistema-de-caja.md)). Con Pagos, el envío incluye el comprobante:
- Incluye grupo, ítems, montos, propina, medio de pago y comprobante. También los pagos por fuera registrados por el mesero.
- Va en un solo sentido; el menú no se sincroniza desde la caja en esta fase.
- **Un solo emisor por venta:** si Hungría emite el comprobante, la caja no lo vuelve a emitir, y viceversa.
- Si el envío falla, se reintenta y la venta queda pendiente de sincronizar.

## Futuro
Historial de visitas y acumulador de boletas dentro de la interfaz del cliente. Solo registrado; no se diseña en esta fase (módulo **Cuenta de cliente**, planeado).
