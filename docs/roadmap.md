# Mapa de avance por módulo

Qué está documentado de cada módulo, dónde está y qué falta. Corte: 2026-11-10. Se actualiza cada vez que se diseña un módulo. Catálogo y paquetes: [módulos](modulos/README.md).

Leyenda: **✔** hecho · **◐** parcial o repartido en otros documentos · **—** no existe todavía · **n/a** no aplica.

## Resumen
| Módulo | Fase | Doc propio | Requisitos | Contratos | Eventos | Estados | Flujos | Degradación | Prototipo | Preguntas abiertas |
|---|---|---|---|---|---|---|---|---|---|---|
| Núcleo | 1 | ✔ | ✔ 7 | ✔ | ✔ 6 | ◐ mesa | ◐ | n/a | ◐ carta | 4 |
| Sala | 1 | ✔ | ✔ 13 | ✔ | ✔ 16 | ✔ pedido, llamado | ✔ 01–05 | ✔ | ✔ | 1 |
| Mesa digital | 1 | ✔ | ✔ 11 | ✔ | ✔ 6 | ◐ sesión | ✔ 01–05 | ✔ | ✔ | 1 |
| Pagos y comprobantes | 1 | ✔ | ✔ 4 | ✔ | ✔ 11 | ✔ pago, reembolso, comprobante | ✔ 04–05 | ✔ | ◐ | 5 |
| Cocina | planeado | — | ✔ 4 | ◐ | ✔ 4 | ✔ ítem | ◐ 02–03 | ✔ | ◐ simulador | 0 |
| Recepción y reservas | 1 | — | ✔ 2 | ◐ | ◐ 2 | — | ◐ 01 | n/a | — | 1 |
| Personal | planeado | — | — | ◐ | ◐ 1 | — | — | ✔ | — | 2 |
| Inventario | planeado | — | — | ◐ | ◐ 2 | — | — | n/a | — | 0 |
| Para llevar | planeado | — | — | — | — | — | — | ✔ | — | 0 |
| Delivery por apps | planeado | — | — | — | — | — | — | ✔ | — | 1 |
| Cupones y promociones | planeado | — | — | — | — | — | — | ✔ | — | 0 |
| Reportes avanzados | planeado | — | — | — | — | — | — | ✔ | — | 0 |
| Cuenta de cliente | futuro | — | — | ◐ | — | — | — | n/a | — | 0 |

Los números son la cantidad de requisitos ([requisitos](plataforma/requisitos.md)), de eventos ([eventos](plataforma/eventos.md)) y de preguntas abiertas ([preguntas abiertas](preguntas-abiertas.md)) de cada módulo.

## Transversal (aplica a todos)
| Tema | Dónde | Estado |
|---|---|---|
| Modularidad y contratos | [ADR 0001](adr/0001-modularidad.md) | ✔ |
| Licencias, paquetes y módulos extra | [ADR 0009](adr/0009-licencias-y-activacion-de-modulos.md), [módulos](modulos/README.md) | ✔ |
| Dependencias y degradación | [dependencias](plataforma/dependencias.md) | ✔ |
| Eventos y comandos | [ADR 0010](adr/0010-eventos-y-comandos.md), [eventos](plataforma/eventos.md) | ✔ |
| Operación sin red | [ADR 0006](adr/0006-operacion-sin-red.md), R15 | ✔ |
| Vía humana en cada paso | [principios](plataforma/principios.md), R16 | ✔ |
| Privacidad (Ley 29733) | [preguntas abiertas](preguntas-abiertas.md) | ◐ decidido cumplirla; falta el cómo |
| Stack y arquitectura | [ADR 0013](adr/0013-stack-y-arquitectura.md) | ◐ backend decidido; frontend pendiente |
| Comparativa con TastyIgniter | [comparativa](comparativa-tastyigniter.md), [ADR 0012](adr/0012-alcance-frente-a-tastyigniter.md) | ✔ |

## Detalle por módulo

### Núcleo
- **Hecho:** [nucleo.md](modulos/nucleo/README.md) con locales y horarios, mesas y zonas, carta (IGV incluido, opciones y extras, cartas por horario), usuarios y roles, licencia, reportes básicos, auditoría, notificaciones, acceso de soporte y automatizaciones. Estados de la mesa en [estados](modulos/sala/estados.md#mesa-núcleo). Claves NFC en [ADR 0011](adr/0011-claves-nfc.md).
- **Falta:** permisos por rol en detalle; plantillas de notificación; catálogo de automatizaciones; modelo de la carta (ítem, opción, extra, horario).
- **Preguntas:** datos al desactivar un módulo, cambio de paquete, proveedor de SMS, privacidad.

### Sala
- **Hecho:** [sala.md](modulos/sala/README.md), [sesión de mesa](modulos/sala/sesion-de-mesa.md), [modos de servicio](modulos/mesa-digital/modos-de-servicio.md), estados de pedido y llamado, los 5 flujos, envío al sistema de caja ([ADR 0007](adr/0007-ventas-al-sistema-de-caja.md)), descuentos y cortesías, prototipo del teléfono del mesero.
- **Falta:** pantallas de la app del mesero en detalle (el prototipo es de baja fidelidad); formato del envío al sistema de caja (depende del piloto).
- **Preguntas:** límite por defecto de los descuentos del mesero.

### Mesa digital
- **Hecho:** [mesa-digital.md](modulos/mesa-digital/README.md), [acceso a la mesa](modulos/mesa-digital/acceso-a-la-mesa.md) ([ADR 0004](adr/0004-acceso-nfc-sdm-y-qr.md)), grupos y nombres de animal, estados de la sesión en [sesión de mesa](modulos/sala/sesion-de-mesa.md#estados-de-la-sesión), los 5 flujos, feedback e invitación a Google, prototipo del teléfono del cliente.
- **Falta:** versión en inglés del prototipo; textos de consentimiento de privacidad.
- **Preguntas:** privacidad (compartida con el Núcleo).

### Pagos y comprobantes
- **Hecho:** [README del módulo](modulos/pagos/README.md) (responsabilidades, contratos, dinero en céntimos, estados del pago, reembolso y comprobante, saldo a favor, interfaces de los adaptadores de pasarela y de PSE/OSE, idempotencia y conciliación); reglas de negocio en [pagos-y-comprobantes.md](modulos/pagos/pagos-y-comprobantes.md); [ADR 0005](adr/0005-piloto-peru-pagos-y-comprobantes.md), [ADR 0008](adr/0008-pasarela-propia-de-cada-restaurante.md); 11 eventos; flujos 04 y 05; cobro en la PWA dentro del prototipo.
- **Falta:** QR de pago del mesero en el prototipo (R23); confirmar los tiempos de vencimiento propuestos.
- **Preguntas:** pasarela del piloto, proveedor PSE/OSE, quién emite en el piloto, reparto de propinas, cierre con comprobante en contingencia.

### Cocina
- **Hecho:** requisitos (R4 estados, R25, R27, R28 comanda), estados del ítem, 4 eventos, contrato con Sala en [sala.md](modulos/sala/README.md), degradación, avance de platos en el simulador del prototipo.
- **Falta:** documento propio; estaciones; pantalla (KDS) e impresora de respaldo en detalle.

### Recepción y reservas
- **Hecho:** requisitos R22 (lista de espera) y R35 (reservas online), 2 eventos, contrato con Sala, lista de espera en el flujo 01.
- **Falta:** documento propio; flujo de reserva online; estados de la reserva; eventos de reserva (creada, confirmada, cancelada, no llegó). Es **fase 1**, así que es el hueco más urgente.
- **Preguntas:** garantía o depósito y qué pasa si el cliente no llega.

### Personal e Inventario
- **Hecho:** contratos con Sala y Cocina, eventos `staff.assignment.changed`, `inventory.item.depleted` e `inventory.item.restocked`, degradación cuando faltan.
- **Falta:** documento propio, requisitos, estados y flujos.
- **Preguntas (Personal):** qué ve el mesero de cada grupo y cuántas alertas, reparto de propinas.

### Para llevar, Delivery por apps, Cupones y promociones, Reportes avanzados
- **Hecho:** alcance en el [catálogo](modulos/README.md#catálogo) y [ADR 0012](adr/0012-alcance-frente-a-tastyigniter.md), matriz y degradación en [dependencias](plataforma/dependencias.md#módulos-extra).
- **Falta:** todo lo demás (documento, requisitos, contratos, eventos, estados, flujos).
- **Preguntas (Delivery):** con qué apps se integra primero.

### Cuenta de cliente
- **Hecho:** alcance (correo, Google o Apple, tarjeta guardada, historial y comprobantes) y contratos con Mesa digital y Pagos.
- **Falta:** todo el diseño. Es futuro.

## Frontend
El stack del frontend está pendiente ([ADR 0013](adr/0013-stack-y-arquitectura.md)). Ruta planeada, sin empezar: [plan de frontend](frontend/plan.md).

## Orden sugerido
1. **Recepción y reservas:** es fase 1 y casi no tiene diseño.
2. **Cocina:** completa el paquete base Mesero.
3. **Personal** e **Inventario.**
4. Módulos extra y Cuenta de cliente.
