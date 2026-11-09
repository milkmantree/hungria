# Requisitos

Lista única de requisitos, con el módulo responsable de cada uno. Los códigos son estables: no se renumeran al mover un requisito de módulo. Los flujos los citan entre paréntesis, por ejemplo (R5).

| # | Requisito | Módulo | Flujos |
|---|---|---|---|
| R1 | Abrir sesión por NFC (SDM, firma y contador validados) o por QR; el QR exige confirmación (pago o mesero) para que el pedido avance | Mesa digital | 01, 02 |
| R2 | Sesión de mesa con grupos; en la PWA cada usuario recibe un nombre anónimo de animal | Sala (sesión y grupos), Mesa digital (nombres) | 01 |
| R3 | Vincular invitados de forma explícita; un comensal en un solo grupo; quien llega tarde puede crear grupo propio o pedir unirse | Mesa digital | 01, 02, 04 |
| R4 | Carta completa con disponibilidad actualizada, búsqueda en la PWA y seguimiento del estado de los platos | Núcleo (carta y disponibilidad), Mesa digital (búsqueda), Cocina (estados) | 02, 03 |
| R5 | Pedido por grupo; alergias y notas siempre revisadas por una persona antes de avanzar | Sala | 02, 03 |
| R6 | Modo Directo: el pago confirma el pedido y lo envía a cocina; cada adición genera un nuevo pago | Mesa digital (requiere Pagos) | 02, 04 |
| R7 | Modo Acompañado: aviso al mesero, confirmación humana, pago al final | Mesa digital (aviso), Sala (confirmación) | 02, 04 |
| R8 | El mesero edita pedidos hasta que la cocina empieza cada ítem (R25), gestiona participantes (expulsar) y fusiona o divide sesiones al unir o separar mesas | Sala | 01–05 |
| R9 | Adiciones en cualquier momento y llamado al mesero con motivo | Sala (adiciones y recepción del llamado), Mesa digital (botón de llamado) | 03 |
| R10 | Plato compartido cargado a un solo grupo; el mesero puede reasignar | Sala | 03 |
| R11 | Pago por fuera siempre disponible; el mesero registra qué quedó pagado; el grupo pasa a modo Acompañado | Sala | 04 |
| R12 | Comprobante SUNAT por grupo vía PSE/OSE: boleta por defecto, factura con RUC; enviado al correo, impreso o a la cuenta del cliente | Pagos (envío a la cuenta: Cuenta de cliente) | 05 |
| R13 | Cerrar la sesión al liquidarse el último grupo; mesa a "por limpiar" | Sala | 05 |
| R14 | Feedback breve y opcional en la PWA; las quejas las atiende una persona | Mesa digital | 05 |
| R15 | Operar sin red: router 4G de respaldo; si no basta, comanda en papel y cobro manual, y el mesero lo registra después ([ADR 0006](../adr/0006-operacion-sin-red.md)) | Todos | todos |
| R16 | Toda acción digital tiene una vía humana equivalente | Todos | todos |
| R17 | PWA en español e inglés, sin instalar nada | Mesa digital (traducciones de la carta: Núcleo) | todos |
| R18 | Cancelar o editar un pedido ya pagado genera saldo a favor del grupo; lo que sobre al cerrar se reembolsa al medio original | Pagos | 02, 04, 05 |
| R19 | Pago digital con los medios de la pasarela del restaurante; propina sugerida del 10%, editable, por grupo | Pagos | 04 |
| R20 | Autodeclaración de mayoría de edad para pedir alcohol; el mesero verifica si tiene dudas | Mesa digital | 02 |
| R21 | Cierre automático de la sesión tras 30 min inactiva, si todo está liquidado o no hubo consumo | Sala | 05 |
| R22 | Lista de espera: registrar al grupo, estimar la espera y avisar cuando la mesa esté por liberarse | Recepción y reservas | 01 |
| R23 | Sin Mesa digital, el mesero genera un QR o link de pago para el grupo | Pagos | 04 |
| R24 | Cada cuenta cerrada se envía al sistema de caja del restaurante, con el comprobante si lo emitió Hungría ([ADR 0007](../adr/0007-ventas-al-sistema-de-caja.md)) | Sala | 04, 05 |
| R25 | Un ítem se puede cancelar solo hasta que la cocina lo empieza; desde ahí se cobra. Con solo impresora, la comanda impresa cuenta como en preparación | Sala, Cocina | 02, 03 |
| R26 | Un llamado sin respuesta se escala al encargado a los 3 min (configurable por local) | Sala | 03 |
| R27 | Alerta de plato demorado al superar un tiempo fijo por local (configurable) | Cocina | 03 |

## Por módulo
| Módulo | Requisitos |
|---|---|
| [Núcleo](nucleo.md) | R4 (carta), R17 (traducciones) |
| [Sala](sala.md) | R2, R5, R7, R8, R9, R10, R11, R13, R21, R24, R25, R26 |
| [Mesa digital](mesa-digital.md) | R1, R2, R3, R4 (búsqueda), R6, R7, R9, R14, R17, R20 |
| [Pagos y comprobantes](../pagos-y-comprobantes.md) | R12, R18, R19, R23 |
| Cocina | R4 (estados), R25, R27 |
| Recepción y reservas | R22 |
| Todos | R15, R16 |
