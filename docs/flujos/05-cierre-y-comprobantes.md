# 05 — Cierre y comprobantes

## Objetivo
Cerrar cada grupo y la sesión con buena impresión, entregar el comprobante donde el cliente prefiera, recoger opinión sin molestar y dejar la mesa lista rápido.

## Actores
Titular, mesero, sistema, encargado.

## Diagrama
```mermaid
flowchart TD
    A[Grupo liquidado] --> R[⚙️ Reembolsar saldo a favor, si queda]
    R --> B[⚙️ Emitir boleta, o factura con RUC, vía PSE/OSE]
    B --> C{¿Destino?}
    C -- cuenta en la app --> D[⚙️ Enviar a la cuenta]
    C -- correo --> E[⚙️ Enviar al correo]
    C -- físico --> F[🤝 Mesero entrega impreso]
    D --> G[🤝 Despedida]
    E --> G
    F --> G
    G --> H[⚙️ Invitación breve a opinar]
    H --> I{¿Opinión negativa?}
    I -- sí --> J[⚙️ Alerta a encargado]
    J --> K[🤝 Persona contacta al cliente]
    I -- no --> L[⚙️ Registrar]
    A --> M{¿Último grupo?}
    M -- sí --> N[⚙️ Sesión cerrada, mesa por limpiar]
    N --> O[🤝 Limpieza y montaje]
    O --> P[⚙️ Mesa libre]
```

## Qué automatiza la tecnología
- Boleta o factura **por grupo**, emitida por un PSE/OSE al liquidarse; factura si el cliente ingresó su RUC. (R12)
- Reembolso automático del saldo a favor que quede al cerrar el grupo. (R18)
- Cierre automático de la sesión tras 30 min inactiva, si todo está liquidado o no hubo consumo. (R21)
- Envío a la cuenta del cliente (si está inscrito), a su correo, o impresión, según indique. (R12)
- Cierre de la sesión cuando se liquida el último grupo y paso de la mesa a "por limpiar". (R13)
- Invitación breve y opcional a dejar feedback; alerta inmediata si es negativo. (R14)

## Dónde el humano es obligatorio
- Despedida y agradecimiento.
- Entregar el comprobante impreso si el cliente lo pidió. (R16)
- Responder a quejas: una persona contacta al cliente. (R14)
- Limpieza y montaje de la mesa.
- Cerrar manualmente una sesión sin consumo o con problemas. (R13)

## Señales digitales / IoT
- Envío de comprobantes, QR o mensaje de feedback, estado de mesa (por limpiar, libre).

## Fallas y excepciones
- Correo inválido o inscripción pendiente: el mesero ofrece alternativa (impreso). (R12)
- Cliente no quiere opinar: no se insiste. (R16)
- Un grupo se va y otro sigue: la sesión permanece abierta hasta el último. (R13)
- Sin red: comprobante impreso manual y emisión electrónica al reconectar. (R15)
- RUC inválido: se emite boleta o el mesero corrige los datos. (R12)
- Falla el reembolso del saldo: alerta al encargado para devolverlo por otra vía. (R18)

## Métricas de calidad
Tiempo de entrega de comprobante, tasa de respuesta de feedback, tiempo de contacto ante una queja, tiempo de rotación de mesa.

## Módulos que toca
Sala (cierre de sesión, envío al sistema de caja); Mesa digital (feedback); Pagos y comprobantes; Cuenta de cliente (futuro, historial); Personal (limpieza, encargado).

## Futuro
Historial de visitas y acumulador de boletas en la interfaz del cliente. Registrado en [pagos y comprobantes](../modulos/pagos/pagos-y-comprobantes.md); no se diseña en esta fase.
