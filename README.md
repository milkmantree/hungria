# Hungría

Codename de una plataforma modular de herramientas digitales y de IoT para gestionar un restaurante.

**Propuesta de valor:** apalancar la tecnología al máximo sin poner en jaque la calidad de la atención. La tecnología quita fricción; las personas ponen el trato.

## Estado

Fase 1 — diseño de los flujos de atención al cliente para un restaurante casual de 10 a 20 mesas. Aún sin código.

## Índice de documentación

- [Visión](docs/vision.md) · [Principios de diseño](docs/plataforma/principios.md) · [Glosario](docs/plataforma/glosario.md)
- Modelo de atención al cliente:
  - [Sesión de mesa](docs/modulos/sala/sesion-de-mesa.md) (grupos, titular, invitados)
  - [Modos de servicio](docs/modulos/mesa-digital/modos-de-servicio.md) (Directo y Acompañado)
  - [Acceso a la mesa](docs/modulos/mesa-digital/acceso-a-la-mesa.md) (NFC con SDM y QR)
  - [Pagos y comprobantes](docs/modulos/pagos/pagos-y-comprobantes.md)
- [Módulos](docs/modulos/README.md): [Núcleo](docs/modulos/nucleo/README.md) · [Sala](docs/modulos/sala/README.md) · [Mesa digital](docs/modulos/mesa-digital/README.md) · [Pagos y comprobantes](docs/modulos/pagos/README.md) · [Dependencias y degradación](docs/plataforma/dependencias.md) · [Requisitos](docs/plataforma/requisitos.md) · [Eventos y comandos](docs/plataforma/eventos.md) · [Máquinas de estado](docs/modulos/sala/estados.md) · [Mapa de avance](docs/roadmap.md)
- [Flujos](docs/flujos/README.md)
  1. [Llegada y acceso](docs/flujos/01-llegada-y-acceso.md)
  2. [Mesa y pedido](docs/flujos/02-mesa-y-pedido.md)
  3. [Servicio](docs/flujos/03-servicio.md)
  4. [Cuenta y pago](docs/flujos/04-cuenta-y-pago.md)
  5. [Cierre y comprobantes](docs/flujos/05-cierre-y-comprobantes.md)
- Decisiones: [0001 Modularidad](docs/adr/0001-modularidad.md) · [0002 Documentación](docs/adr/0002-documentacion.md) · [0003 Sesión de mesa con grupos](docs/adr/0003-sesion-de-mesa-con-grupos.md) · [0004 Acceso NFC SDM y QR](docs/adr/0004-acceso-nfc-sdm-y-qr.md) · [0005 Piloto en Perú](docs/adr/0005-piloto-peru-pagos-y-comprobantes.md) · [0006 Operación sin red](docs/adr/0006-operacion-sin-red.md) · [0007 Ventas al sistema de caja](docs/adr/0007-ventas-al-sistema-de-caja.md) · [0008 Pasarela propia de cada restaurante](docs/adr/0008-pasarela-propia-de-cada-restaurante.md) · [0009 Licencias y activación de módulos](docs/adr/0009-licencias-y-activacion-de-modulos.md) · [0010 Eventos y comandos](docs/adr/0010-eventos-y-comandos.md) · [0011 Claves NFC](docs/adr/0011-claves-nfc.md) · [0012 Alcance frente a TastyIgniter](docs/adr/0012-alcance-frente-a-tastyigniter.md) · [0013 Stack y arquitectura](docs/adr/0013-stack-y-arquitectura.md)
- [Prototipo navegable](docs/prototipo.md) (cliente y mesero)
- [Plan de frontend](docs/frontend/plan.md) (UX/UI, Impeccable y Astryx)
- [Comparativa con TastyIgniter](docs/comparativa-tastyigniter.md)
- [Preguntas abiertas](docs/preguntas-abiertas.md)
