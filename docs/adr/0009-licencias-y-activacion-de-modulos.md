# ADR 0009 — Licencias y activación de módulos

- Fecha: 2026-11-09
- Estado: aceptado

## Contexto
Hungría se ofrece a la medida: un cliente puede querer solo la operación del mesero y otro el autoservicio en mesa con todo integrado. Los documentos asumían que todos los módulos estaban activos.

Se tomó como referencia la arquitectura de **TastyIgniter** (sistema de restaurantes de código abierto): núcleo pequeño, funciones como extensiones que declaran sus dependencias, y activación y configuración por local. Es una referencia de arquitectura; no se reutiliza su código.

## Decisión
- **Núcleo siempre activo** para todo cliente: restaurante y locales, mesas y zonas, carta, usuarios y roles, licencia, reportes básicos de ventas, auditoría de acciones y automatizaciones.
- **El resto son módulos** que se activan según la licencia: Sala, Mesa digital, Pagos y comprobantes, Cocina, Personal, Inventario y Cuenta de cliente.
- **Atención al cliente se divide en dos módulos:**
  - **Sala:** operación del mesero (toma de pedidos, sesión de mesa, cuenta, pago por fuera).
  - **Mesa digital:** PWA del cliente, acceso NFC/QR, grupos autónomos y modos Directo y Acompañado.
- **Sala y Cocina siempre van juntos.** Son módulos distintos (usuarios y evolución propios), pero se activan como una unidad.
- **Mesa digital sin Pagos** se permite solo en modo Acompañado, con pago por fuera.
- **La licencia es por local.** Cada local de un restaurante tiene sus propios módulos activos. El modelo soporta varios locales por restaurante desde el diseño.
- **Venta por paquetes con módulos extra.** Paquetes base:

| Paquete | Módulos |
|---|---|
| Mesero | Núcleo + Sala + Cocina |
| Mesero con cobro | Mesero + Pagos |
| Mesa digital | Mesero + Mesa digital + Pagos |
| Completo | Todos los módulos |

  A cualquier paquete se le pueden sumar módulos extra, siempre que cumplan sus dependencias.
- **Cada módulo declara** qué módulos necesita, cuáles son opcionales y qué hace cuando un opcional no está activo.
- **Activar un módulo es configuración, no código distinto por cliente.** Todos los clientes usan la misma versión de Hungría.

Detalle: [módulos](../modulos/README.md).

## Consecuencias
- Cada flujo debe funcionar con solo los módulos de su paquete; la degradación se documenta por módulo.
- Los eventos entre módulos deben tolerar que nadie los escuche (módulo no licenciado).
- La documentación de atención al cliente se reorganiza en Sala y Mesa digital.
- La carta pasa al Núcleo porque la usan Sala, Mesa digital, Cocina e Inventario.
- Hay que resolver qué pasa con los datos de un módulo cuando se desactiva.
