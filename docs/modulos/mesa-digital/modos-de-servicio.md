# Modos de servicio

Cada restaurante elige el modo según la atención que quiera dar. Hay dos; el pago por fuera existe en ambos.

## Comparación
| | **Directo** | **Acompañado** |
|---|---|---|
| Idea | Autonomía del cliente, mínima espera | Atención cálida y conversación con el mesero |
| Cómo se pide | El titular elige, agrupa a sus invitados y **paga en la app** | El grupo arma el pedido y **avisa al mesero** |
| Qué confirma el pedido | **El pago** | **La confirmación del mesero** |
| Cuándo llega a cocina | Al pagar | Cuando el mesero confirma |
| Cuándo se paga | Por adelantado, en cada pedido | Al final de la visita, como un restaurante tradicional |
| Adiciones | Cada una genera un nuevo pago | Se avisa al mesero y se añaden a la cuenta |
| Rol del mesero | Entrega, revisa, atiende llamados y puede editar | Confirma, recomienda, conversa, cobra |
| Riesgo | Demasiado casual para algunos locales | Más dependencia de la disponibilidad del mesero |

## Reglas comunes a ambos modos
- **El mesero puede editar los pedidos de la mesa** hasta que la cocina empieza cada ítem; desde ahí el ítem se cobra.
- **Pago por fuera siempre disponible** (POS externo, efectivo, otro medio): el cliente llama al mesero, se arreglan, y el mesero **registra qué quedó pagado**. Un grupo que paga por fuera se comporta desde ese momento como en modo Acompañado.
- **Llamar al mesero** está siempre disponible por múltiples motivos (duda, problema, cuenta, otro).
- Alergias y notas siempre las revisa una persona antes de que el pedido avance (ver [principios](../../plataforma/principios.md)).

## Entrada por QR
El QR es más débil que el NFC ([acceso a la mesa](acceso-a-la-mesa.md)). Su protección es la confirmación: en Directo, el pedido no sale sin pago; en Acompañado, no sale sin el mesero.

Salvaguarda por restaurante, **activada por defecto**: en Directo vía QR, avisar al mesero de la zona de cada pedido nuevo. Es visibilidad, no aprobación; el mesero puede cancelar o editar mientras la cocina no haya empezado los ítems, y el monto queda como saldo a favor del grupo ([pagos](../pagos/pagos-y-comprobantes.md)). El restaurante puede apagarla.

## Alcohol y menores de edad
Para pedir alcohol, el cliente **autodeclara en la PWA** que es mayor de 18 años. El mesero verifica al entregar si tiene dudas y puede cancelar el ítem.

## Cómo elegir
- **Directo** si prima la rapidez, hay poco personal o el local es de ritmo alto.
- **Acompañado** si el restaurante vende trato cercano o recomendación del mesero.
- El piloto soporta ambos modos ([ADR 0005](../../adr/0005-piloto-peru-pagos-y-comprobantes.md)).
- El modo es configuración del restaurante; cambiarlo no debe requerir cambios en el resto de los módulos.
