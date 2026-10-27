# ADR 0004 — Acceso a la mesa por NFC con SDM y QR con confirmación

- Fecha: 2026-10-26
- Estado: aceptado

## Contexto
Hay que abrir la sesión de mesa sin fricción, pero evitando que alguien opere una mesa en la que no está. Un QR impreso es estático y se puede fotografiar. Un NFC común también guarda una URL fija.

## Decisión
- **NFC:** stickers NTAG 424 DNA con SDM/SUN. Cada lectura produce una URL única con UID, contador y firma (CMAC AES-128), validada en el servidor. Da prueba de presencia sin necesidad de reescribir el tag.
- **QR:** se acepta como alternativa. Permite explorar y armar el pedido sin fricción; la **confirmación** es la barrera (pago en Directo, mesero en Acompañado).
- **Sin código corto de mesa.**
- Salvaguarda opcional por restaurante: aviso al mesero de la zona en pedidos Directo vía QR.

Detalle: [acceso a la mesa](../acceso-a-la-mesa.md).

## Consecuencias
- Requiere programar los stickers (activar SDM, claves propias) al instalarlos.
- El QR sigue siendo más débil: un pedido falso en Directo exige pago real del que lo hace.
- La URL del toque solo abre o une; la sesión ya abierta usa su propio token.
- Costo por mesa bajo (unos pocos USD por sticker).
