# ADR 0007 — Hungría pasa las ventas al sistema de caja del restaurante

- Fecha: 2026-11-06
- Estado: aceptado

## Contexto
Muchos restaurantes ya usan un sistema de caja (software POS) para llevar ventas, caja y contabilidad. Hungría cobra y emite comprobantes por su cuenta, así que sin integración el restaurante tendría las ventas repartidas en dos sistemas.

Se evaluaron tres caminos: Hungría funciona aparte, Hungría pasa las ventas al sistema de caja, o integración completa en ambos sentidos (menú y pedidos sincronizados).

## Decisión
- Hungría **envía cada venta liquidada** al sistema de caja del restaurante: grupo, ítems, montos, propina, medio de pago y comprobante emitido.
- El envío es **en un solo sentido**. El menú y los pedidos no se sincronizan desde el sistema de caja en esta fase.
- **Un solo emisor de comprobantes por venta.** Si Hungría emite la boleta o factura, el sistema de caja la registra sin volver a emitirla. Si el restaurante prefiere que emita el sistema de caja, Hungría no emite.
- Los pagos por fuera que registra el mesero también se envían, para que la caja cuadre.
- Si el envío falla, se reintenta y la venta queda marcada como pendiente de sincronizar.

Detalle: [pagos y comprobantes](../pagos-y-comprobantes.md).

## Actualización 2026-11-09
Con las licencias por módulo ([ADR 0009](0009-licencias-y-activacion-de-modulos.md)), el envío lo hace el módulo **Sala**, tenga o no el local el módulo Pagos. Sin Pagos, Hungría no emite comprobantes: los emite el sistema actual del restaurante, y el envío va sin comprobante.

## Consecuencias
- El restaurante tiene sus ventas y su contabilidad en un solo lugar.
- Depende de que el sistema de caja del piloto tenga API o permita importar ventas. Si no la tiene, la alternativa es exportar las ventas en un archivo para importarlas.
- El envío se hace a través de un adaptador por cada sistema de caja, para no acoplar Hungría a uno en particular ([ADR 0001](0001-modularidad.md)).
- Hay que conciliar diariamente lo enviado con lo registrado en caja.
