# Módulo: Atención al cliente

Estado: fase 1, diseño. Cubre el recorrido completo del cliente en torno a la [sesión de mesa](../sesion-de-mesa.md) y los [modos de servicio](../modos-de-servicio.md). Flujos en [../flujos/](../flujos/README.md).

## Responsabilidades
- Gestionar llegada, lista de espera y apertura de la sesión de mesa (NFC/QR).
- Administrar grupos, titulares, invitados vinculados y la identidad anónima de la sesión.
- Capturar pedidos por grupo y llevarlos a cocina según el modo (pago o confirmación del mesero).
- Atender adiciones, llamados y platos compartidos; permitir al mesero editar y reasignar.
- Coordinar el cierre por grupo y el de la sesión; entregar comprobantes mediante el módulo de pagos.
- Recoger feedback y dejar la mesa lista.

## Requisitos derivados de los flujos
| # | Requisito | Flujo |
|---|---|---|
| R1 | Abrir sesión por NFC (SDM, firma y contador validados) o por QR; el QR exige confirmación (pago o mesero) para que el pedido avance | 01, 02 |
| R2 | Sesión de mesa con grupos; cada usuario recibe nombre anónimo de animal | 01 |
| R3 | Vincular invitados de forma explícita; un comensal en un solo grupo; llegada tardía puede crear grupo propio o pedir unirse | 01, 02, 04 |
| R4 | Carta completa con búsqueda, disponibilidad actualizada y seguimiento del estado de los platos | 02, 03 |
| R5 | Pedido por grupo; alergias y notas siempre revisadas por una persona antes de avanzar | 02, 03 |
| R6 | Modo Directo: el pago confirma el pedido y lo envía a cocina; cada adición genera un nuevo pago | 02, 04 |
| R7 | Modo Acompañado: aviso al mesero, confirmación humana, pago al final | 02, 04 |
| R8 | El mesero edita pedidos en todo momento, gestiona participantes (expulsar) y resuelve reembolsos | 01–05 |
| R9 | Adiciones en cualquier momento y llamado al mesero con motivo | 03 |
| R10 | Plato compartido cargado a un solo grupo; el mesero puede reasignar | 03 |
| R11 | Pago por fuera siempre disponible; el mesero registra qué quedó pagado; el grupo pasa a modo Acompañado | 04 |
| R12 | Comprobante (boleta o factura) por grupo, enviado a la cuenta, al correo o impreso | 05 |
| R13 | Cerrar la sesión al liquidarse el último grupo; mesa a "por limpiar" | 05 |
| R14 | Feedback breve y opcional; las quejas las atiende una persona | 05 |
| R15 | Operar sin red: comanda en papel y cobro manual, reconciliar después | todos |
| R16 | Toda acción digital tiene una vía humana equivalente | todos |

## Contratos con otros módulos (a definir)
| Con | Atención al cliente envía | Atención al cliente recibe |
|---|---|---|
| Cocina | comanda (ítems, notas, alergias, mesa, grupo) | estado por plato (recibido, en preparación, listo) |
| Inventario | consumo por ítem vendido | disponibilidad del menú (ítems agotados) |
| Personal | llamados y alertas por mesa/zona | asignación de mesas/zonas por turno |
| Pagos y comprobantes | cargo por grupo, pagos por fuera registrados por el mesero | confirmación de pago, comprobante emitido |
| Cuenta de cliente (futuro) | identidad opcional del cliente, destino de comprobantes | historial de visitas |

## Preguntas abiertas
Ver [../preguntas-abiertas.md](../preguntas-abiertas.md).
