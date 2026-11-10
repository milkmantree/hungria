# Máquinas de estado

Estados de las entidades de Sala, Mesa digital y Cocina. Los de la sesión y el grupo están en [sesión de mesa](sesion-de-mesa.md). Cada cambio de estado se publica como evento ([eventos](../../plataforma/eventos.md)).

## Mesa (Núcleo)
```mermaid
stateDiagram-v2
    [*] --> Libre
    Libre --> Ocupada: se abre una sesión
    Ocupada --> PorLimpiar: se cierra la sesión
    PorLimpiar --> Libre: limpieza y montaje
    Libre --> FueraDeServicio: encargado la bloquea
    FueraDeServicio --> Libre: encargado la habilita
```
- Al unir mesas, todas quedan **Ocupada** bajo una sola sesión; al cerrarla, todas pasan a **PorLimpiar**.
- Evento: `core.table.status_changed`.

## Pedido (Sala)
Un pedido es lo que un grupo envía de una vez. Su recorrido hasta cocina depende del modo y de quién lo arma.

```mermaid
stateDiagram-v2
    [*] --> Borrador: el grupo arma el pedido en la PWA
    [*] --> Confirmado: el mesero lo toma en su dispositivo
    Borrador --> PorConfirmar: envía (Acompañado)
    Borrador --> PorPagar: envía (Directo)
    PorPagar --> Confirmado: pago aprobado
    PorPagar --> Borrador: pago rechazado
    PorConfirmar --> Confirmado: mesero confirma o edita
    Borrador --> Cancelado: el cliente lo descarta
    PorConfirmar --> Cancelado: cliente o mesero
    Confirmado --> EnCocina: comanda enviada
    EnCocina --> [*]: sigue por ítem
    Cancelado --> [*]
```
- Las alergias y notas se revisan antes de pasar a **Confirmado** (R5).
- Desde **EnCocina**, cada ítem sigue su propio estado.

## Ítem del pedido (Cocina)
```mermaid
stateDiagram-v2
    [*] --> Recibido: llega a cocina
    Recibido --> EnPreparacion: cocina lo empieza
    EnPreparacion --> Listo
    Listo --> Entregado: mesero lo lleva a la mesa
    Recibido --> Cancelado: mesero, con motivo
    Entregado --> [*]
    Cancelado --> [*]
```
- **Cancelar:** solo hasta **Recibido**. Desde **EnPreparacion** el ítem se cobra (R25).
- **Solo impresora:** si la cocina no usa pantalla, la comanda impresa cuenta como **EnPreparacion**.
- **Pagado en Directo y cancelado:** el monto queda como saldo a favor del grupo (R18).
- **Demora:** si un ítem no llega a **Listo** dentro del tiempo fijo del local (configurable, por ejemplo 20 min) desde **Recibido**, se emite `kitchen.item.delayed` y se alerta al mesero (R27). No cambia de estado.
- Evento: `kitchen.item.status_changed`.

## Llamado (Sala)
```mermaid
stateDiagram-v2
    [*] --> Abierto: el cliente llama desde la PWA
    Abierto --> Atendiendo: un mesero lo toma
    Abierto --> Escalado: 3 min sin respuesta
    Escalado --> Atendiendo: mesero o encargado lo toma
    Atendiendo --> Resuelto
    Abierto --> Cancelado: el cliente lo retira
    Resuelto --> [*]
    Cancelado --> [*]
```
- **Abierto:** avisa al mesero de la zona, o a todos los meseros del local sin Personal.
- **Escalado:** a los 3 minutos (configurable por local) alerta también al encargado (R26).
- Eventos: `tableside.call.requested`, `floor.call.escalated`, `floor.call.answered`.
