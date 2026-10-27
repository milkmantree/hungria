# Módulos

Hungría se compone de módulos independientes (ver [ADR 0001](../adr/0001-modularidad.md)).

| Módulo | Estado | Responsabilidad |
|---|---|---|
| [Atención al cliente](atencion-cliente.md) | fase 1, diseño | Sesión de mesa, grupos, pedido, servicio, cierre |
| Pagos y comprobantes | planeado | Cobro por grupo, pagos por fuera, boletas y facturas (ver [pagos](../pagos-y-comprobantes.md)) |
| Cuenta de cliente | planeado, futuro | Perfil opcional, destino de comprobantes, historial de visitas |
| Cocina | planeado | Recibir comandas, tiempos de preparación, estaciones |
| Personal | planeado | Turnos, asignación de mesas/zonas, comunicación interna |
| Inventario | planeado | Existencias, consumo por plato, disponibilidad del menú |

Los módulos planeados no tienen documento propio hasta que se aborden; sus contratos con atención al cliente están en [atencion-cliente.md](atencion-cliente.md).

## Dependencias (contratos)
```mermaid
flowchart LR
    AC[Atención al cliente] -->|comandas| CO[Cocina]
    CO -->|estado del plato| AC
    AC -->|consumo| IN[Inventario]
    IN -->|disponibilidad del menú| AC
    PE[Personal] -->|asignación de zonas| AC
    AC -->|llamados y alertas| PE
    AC -->|cargos y pagos por fuera| PA[Pagos y comprobantes]
    PA -->|pago confirmado, comprobante| AC
    PA -->|comprobantes| CC[Cuenta de cliente]
```
