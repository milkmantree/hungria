# Prototipo navegable

Pantallas en baja fidelidad de la PWA del cliente y la app del mesero, con el registro en vivo de los [eventos y comandos](modulos/eventos.md) que dispara cada acción.

- Enlace: https://claude.ai/artifact/SviQ9JW375tqVunknrRXKP (privado; se comparte desde el menú Compartir de la página).
- Paquete que muestra: **Mesa digital** (Núcleo, Sala, Cocina, Mesa digital y Pagos), sin Personal ni Inventario.
- Mesa 7 de un restaurante en Lima, con modo Directo o Acompañado.

## Qué se puede recorrer
| Cliente (Mesa digital) | Mesero (Sala) |
|---|---|
| Acceso por NFC, nombre de animal, crear grupo o pedir unirse | Mapa de mesas con avisos |
| Carta con búsqueda, agotados, alérgenos y autodeclaración para alcohol | Confirmar pedidos y revisar alergias y notas (R5) |
| Pedido con notas; avisar al mesero (Acompañado) o pagar (Directo) | Cancelar ítems solo hasta que cocina empieza (R25) |
| Seguimiento por plato, saldo a favor, llamado al mesero con motivo | Atender llamados; escalado al encargado a los 3 min (R26) |
| Cuenta, propina del 10%, medios de pago, pago con el mesero | Registrar pago por fuera (efectivo o POS) |
| Boleta o factura con RUC, correo o impreso, feedback | Entregar platos listos, ver feedback negativo, liberar la mesa |

El simulador del centro avanza los platos en cocina y adelanta el reloj.

## Límites
- Solo español; la PWA final es bilingüe (R17).
- Unirse a un grupo existente muestra la solicitud, pero el recorrido sigue con un grupo propio.
- No muestra los paquetes Mesero ni Mesero con cobro (por ejemplo, el QR de pago del mesero, R23).
