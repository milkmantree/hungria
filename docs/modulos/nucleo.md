# Núcleo

Estado: fase 1, diseño. Siempre activo en todo local ([ADR 0009](../adr/0009-licencias-y-activacion-de-modulos.md)). Es la base que usan todos los módulos; no depende de ninguno.

## Responsabilidades
- **Restaurante y locales:** datos del restaurante, sus locales, su horario de atención y la configuración de cada uno.
- **Mesas y zonas:** mesas de cada local, sus zonas y su estado (libre, abierta, por limpiar). Los stickers NFC y los QR se asocian a la mesa aquí; el encargado puede desactivar un sticker ([ADR 0011](../adr/0011-claves-nfc.md)).
- **Carta:** ítems, precios con IGV incluido, categorías, alérgenos, traducciones (español e inglés) y disponibilidad. Sin Inventario, el personal marca a mano los ítems agotados.
  - **Opciones de plato:** obligatorias (elegir una, por ejemplo el punto del lomo) y extras opcionales con precio.
  - **Cartas por horario** (desayuno, almuerzo, cena) según el horario de atención del local.
- **Usuarios y roles:** personal del local (encargado, mesero, cocina, anfitrión) y sus permisos.
- **Licencia:** módulos activos en cada local y validación de sus dependencias ([dependencias](dependencias.md)).
- **Reportes básicos de ventas:** ventas por día, por mesa y por medio de pago.
- **Auditoría de acciones:** quién editó, canceló, cobró, reembolsó, regaló o descontó qué y cuándo.
- **Notificaciones** al cliente por correo y SMS, con plantillas por tipo de aviso (pedido listo para recoger, reserva confirmada, comprobante).
- **Acceso de soporte:** el restaurante autoriza a soporte de Hungría por tiempo limitado; queda en la auditoría y no incluye datos de pago.
- **Automatizaciones:** reglas del tipo "cuando pase X, haz Y" sobre los eventos de los módulos activos.

## Requisitos
R4 (carta y disponibilidad), R17 (traducciones de la carta), R28, R29, R30, R32, R33. Ver [requisitos](requisitos.md).

## Qué ofrece a los módulos
| A | Ofrece |
|---|---|
| Todos | Locales, mesas y zonas, usuarios y roles, licencia activa, registro de auditoría, automatizaciones |
| Sala, Mesa digital, Cocina | Carta y disponibilidad |
| Inventario | Carta (para vincular ítems con existencias); recibe de vuelta la disponibilidad |

## Qué recibe de los módulos
- Eventos de todos los módulos para auditoría, reportes y automatizaciones.
- Cuentas cerradas de Sala, para los reportes básicos.
