# ADR 0008 — Cada restaurante conecta su propia pasarela de pagos

- Fecha: 2026-11-06
- Estado: aceptado

## Contexto
Hungría cobra en la PWA ([ADR 0005](0005-piloto-peru-pagos-y-comprobantes.md)). Había que decidir si usaba una sola pasarela para todos los restaurantes o si cada restaurante traía la suya.

## Decisión
- **Requisito para cobrar en la PWA:** cada restaurante debe tener una **cuenta propia con API** en alguna pasarela que opere en Perú (por ejemplo Culqi, Izipay, Niubiz o Mercado Pago).
- Hungría **no cobra a nombre del restaurante** ni recibe su dinero: los pagos van directo a la cuenta del restaurante.
- Hungría soporta varias pasarelas mediante **un adaptador por pasarela** con un contrato común: cobrar, reembolsar y consultar estado ([ADR 0001](0001-modularidad.md)).
- La PWA muestra **solo los medios que soporta la pasarela del restaurante** (tarjetas, Yape, Plin, Apple Pay, Google Pay).
- Las credenciales de la pasarela las configura el restaurante; se guardan cifradas y **nunca** se versionan.
- Un restaurante sin pasarela puede usar Hungría solo en modo Acompañado y con pago por fuera.

## Consecuencias
- Hungría no maneja fondos de terceros, lo que reduce su carga legal y de riesgo.
- Las comisiones, la liquidación y los reembolsos dependen del contrato de cada restaurante con su pasarela.
- Cada pasarela nueva exige construir y mantener su adaptador. El piloto empieza con la pasarela que use el restaurante piloto.
- El modo Directo exige pasarela, porque el pago es lo que confirma el pedido.
