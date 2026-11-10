# ADR 0011 — Gestión de claves de los stickers NFC

- Fecha: 2026-11-09
- Estado: aceptado

## Contexto
Los stickers NTAG 424 DNA firman cada lectura con una clave AES-128 ([ADR 0004](0004-acceso-nfc-sdm-y-qr.md)). El servidor necesita esa misma clave para validar la firma. Había que definir cómo se generan, dónde se guardan, quién programa los stickers y qué pasa si uno se pierde.

## Decisión
- **Clave derivada por sticker:** cada sticker tiene una clave distinta, calculada a partir de una **clave maestra** y el UID del sticker (diversificación de claves, método documentado por NXP). Extraer la clave de un sticker no sirve para los demás.
- **Una clave maestra por restaurante**, guardada en un **servicio de gestión de claves (KMS)** en la nube que nunca la deja salir. El servidor pide al KMS validar o derivar; la maestra no se copia a ningún otro lugar.
- **Hungría programa los stickers** antes de entregarlos: activa SDM, carga la clave derivada, cambia las claves de fábrica y asocia cada sticker a su mesa en el Núcleo. Las claves nunca pasan por el local.
- **Sticker dañado, perdido o despegado:** el encargado lo **desactiva** en el Núcleo y se pide un reemplazo. Mientras tanto la mesa funciona con su QR. No hay rotación periódica; la clave cambia solo al reemplazar el sticker.
- Nada de esto se versiona en el repo: ni claves, ni UIDs asociados a claves, ni configuraciones del KMS con secretos.

Detalle: [acceso a la mesa](../modulos/mesa-digital/acceso-a-la-mesa.md).

## Consecuencias
- Hungría necesita un puesto de programación (lector NFC y herramienta propia) y un proceso de envío de stickers a cada restaurante.
- Validar un toque requiere el KMS; si no responde, la mesa pasa a QR o al mesero ([ADR 0006](0006-operacion-sin-red.md)).
- Un sticker desactivado se rechaza aunque su firma sea válida.
- Reponer stickers toma días (envío), no minutos; el QR cubre ese tiempo.
