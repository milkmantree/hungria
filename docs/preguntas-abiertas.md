# Preguntas abiertas

Pendientes por resolver antes de fijar detalles. Lo ya decidido está en [sesión de mesa](modulos/sala/sesion-de-mesa.md), [modos de servicio](modulos/mesa-digital/modos-de-servicio.md), [pagos y comprobantes](modulos/pagos/pagos-y-comprobantes.md) y los [ADR](adr/).

## Pagos y legal
- ¿Qué pasarela usa el restaurante piloto? Define el primer adaptador. Candidatas: Culqi, Izipay, Niubiz, Mercado Pago. Falta confirmar cuáles soportan Apple Pay y Google Pay.
- ¿Qué proveedor PSE/OSE se usa para emitir comprobantes?
- ¿Cómo se reparte la propina entre el personal? (módulo Personal)
- Privacidad: ya se decidió cumplir la Ley 29733 y su reglamento. Falta definir cómo: textos de consentimiento, registro del banco de datos y plazos de conservación.

## Operación y tecnología
- ¿Qué sistema de caja usa el piloto y tiene API o importación de ventas?
- ¿Quién emite los comprobantes en el piloto: Hungría o el sistema de caja?

## Sala y Cocina
- ¿Cuál es el límite por defecto de los descuentos del mesero?

## Nuevos módulos y canales
- ¿Con qué apps de delivery se integra primero (Rappi, PedidosYa) y qué permiten sus API?
- ¿Qué proveedor de SMS se usa?
- Reservas: ¿se pide garantía o depósito? ¿Qué pasa si el cliente no llega?

## Licencias y módulos
- ¿Qué pasa con los datos de un módulo cuando el local lo desactiva (se conservan, se ocultan, se exportan)?
- ¿Se puede cambiar de paquete en cualquier momento o solo al renovar?

## Para el módulo Personal
- ¿Qué información ve el mesero de cada grupo y cuántas alertas es razonable? El contrato con Sala (llamados y alertas por mesa o zona) ya está en [sala.md](modulos/sala/README.md).

## Resueltas
Ver [ADR 0005](adr/0005-piloto-peru-pagos-y-comprobantes.md) y [ADR 0006](adr/0006-operacion-sin-red.md).

2026-11-05:
- Modo del piloto: ambos, configurable.
- País: Perú; comprobantes SUNAT vía PSE/OSE, boleta por defecto y factura con RUC desde la PWA.
- Interfaz: solo PWA, en español e inglés.
- Medios de pago: tarjetas, Yape, Plin, Apple Pay y Google Pay.
- Propinas: sugeridas por grupo al pagar, 10% por defecto y editable.
- Reembolsos: saldo a favor en la sesión; lo que sobre se reembolsa al medio original al cerrar.
- Inactividad: cierre automático a los 30 min, si todo está liquidado o no hubo consumo.
- Unir o dividir mesas: el mesero fusiona o mueve sesiones.
- Alcohol: autodeclaración en la PWA.
- Aviso al mesero en pedidos Directo por QR: activado por defecto.
- Cocina: pantalla (KDS) con impresora de respaldo.
- Sin red: router 4G de respaldo, papel y reconciliación posterior.
- Grupos y usuarios por sesión: sin límite por defecto, ajustable por restaurante.
- Privacidad: cumplir la Ley 29733 y su reglamento.

2026-11-06:
- Sistema de caja: Hungría le envía las ventas liquidadas, en un solo sentido ([ADR 0007](adr/0007-ventas-al-sistema-de-caja.md)).
- Pasarela: cada restaurante conecta su propia cuenta con API en una pasarela que opere en Perú ([ADR 0008](adr/0008-pasarela-propia-de-cada-restaurante.md)).

2026-11-09 ([ADR 0009](adr/0009-licencias-y-activacion-de-modulos.md)):
- Núcleo siempre activo, con reportes básicos, auditoría y automatizaciones.
- Licencia por local; varios locales por restaurante desde el diseño.
- Venta por paquetes con módulos extra.
- Atención al cliente se divide en Sala y Mesa digital; Sala y Cocina siempre juntos.
- Lista de espera: nuevo módulo Recepción y reservas. Feedback: Mesa digital. Requisitos con códigos estables en [requisitos.md](plataforma/requisitos.md).
- Mesa digital sin Pagos solo en modo Acompañado.
- Sin Pagos, el comprobante lo emite el sistema actual del restaurante.
- El envío al sistema de caja lo hace Sala, con o sin Pagos.
- Pagos sin Mesa digital: el mesero genera un QR o link de pago.
- Sin Personal, los llamados y alertas llegan a todos los meseros del local.
- Detalle: [dependencias y degradación](plataforma/dependencias.md).

2026-11-09 ([ADR 0010](adr/0010-eventos-y-comandos.md)):
- Eventos y comandos entre módulos; nombres `modulo.entidad.verbo` en inglés.
- Eventos con datos mínimos y sin datos personales; entrega al menos una vez con ID único.

2026-11-09 ([máquinas de estado](modulos/sala/estados.md)):
- No se cancela un ítem que la cocina ya empezó; se cobra.
- Llamado sin respuesta: se escala al encargado a los 3 min, configurable.
- Plato demorado: tiempo fijo por local, configurable.
- Directo: el grupo que pagó todo queda "al día" y el comprobante se emite al liquidarse.

2026-11-09 ([ADR 0011](adr/0011-claves-nfc.md)):
- Claves NFC derivadas por sticker desde una clave maestra por restaurante, guardada en un KMS.
- Hungría programa los stickers; si uno falla, se desactiva y se reemplaza, sin rotación periódica.

2026-11-09 ([ADR 0012](adr/0012-alcance-frente-a-tastyigniter.md), comparativa con TastyIgniter):
- Error del local con un ítem en preparación: cortesía del encargado.
- Opciones y extras de plato, cartas por horario, IGV incluido sin recargo.
- Módulos extra nuevos: Para llevar, Delivery por apps, Cupones y promociones, Reportes avanzados.
- Reservas online en la fase 1; feedback privado; notificaciones por correo y SMS; sin API pública; soporte con acceso autorizado.
