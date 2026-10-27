# Módulo: Atención al cliente

Estado: fase 1, diseño. Cubre el recorrido completo del cliente. Flujos en [../flujos/](../flujos/README.md).

## Responsabilidades
- Gestionar llegada, lista de espera y asignación de mesa.
- Capturar pedidos (por mesero o por el cliente) y enviarlos a cocina.
- Dar seguimiento al servicio y atender llamados.
- Calcular y cobrar la cuenta (dividida o no).
- Recoger feedback y cerrar la visita.

## Requisitos derivados de los flujos
| # | Requisito | Flujo |
|---|---|---|
| R1 | Registrar grupo y estimar espera; avisar al cliente sin que deba quedarse en la puerta | 01 |
| R2 | Asignar mesa con apoyo del sistema; el anfitrión puede sobreescribir | 01 |
| R3 | Pedido por mesero o por cliente, con alergias y notas obligatorias de revisar | 02 |
| R4 | Enviar comanda a cocina y seguir su estado | 02, 03 |
| R5 | Llamado de atención sin app (botón de mesa) y con ella | 03 |
| R6 | Cuenta dividible, varios medios de pago, mesero presente en el cierre | 04 |
| R7 | Feedback breve y opcional; quejas escaladas a una persona | 05 |
| R8 | Operar sin red: comanda en papel y cobro manual, reconciliar después | todos |
| R9 | Toda acción digital tiene vía humana equivalente | todos |

## Contratos con otros módulos (a definir)
| Con | Atención al cliente envía | Atención al cliente recibe |
|---|---|---|
| Cocina | comanda (ítems, notas, alergias, mesa) | estado por plato (recibido, en preparación, listo) |
| Inventario | consumo por ítem vendido | disponibilidad del menú (ítems agotados) |
| Personal | llamados y alertas por mesa/zona | asignación de mesas/zonas por turno |

## Preguntas abiertas
Ver [../preguntas-abiertas.md](../preguntas-abiertas.md).
