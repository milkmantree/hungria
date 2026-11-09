# Acceso a la mesa (NFC y QR)

Cada mesa tiene un sticker NFC y un QR propios de esa mesa. Decisión: [ADR 0004](adr/0004-acceso-nfc-sdm-y-qr.md).

## Dos vías, distinta garantía
| | **NFC con SDM** | **QR** |
|---|---|---|
| Qué es | Sticker NTAG 424 DNA que genera una URL distinta en cada lectura | Código impreso con enlace fijo de la mesa |
| Prueba de presencia | Sí: un toque válido y reciente implica estar en la mesa | No: una foto del QR sirve desde cualquier lugar |
| Experiencia | Un toque, sin pasos extra | Escanear; sin pasos extra para explorar y armar pedido |
| Protección | Firma y contador del chip | La **confirmación del pedido** (pago en Directo, mesero en Acompañado) |

No se usa código corto de mesa (descartado).

## NFC con SDM
- Chip: **NTAG 424 DNA** (o su variante **TagTamper**, que además detecta si el sticker fue despegado). Variantes NTAG 22x DNA también ofrecen SUN con menos memoria.
- Con **Secure Dynamic Messaging (SDM/SUN)** el propio chip, al ser leído, genera una URL con UID + contador de lecturas + firma (CMAC, AES-128). No hace falta escribir el tag para rotar el enlace.
- El servidor conoce la clave, valida la firma y exige que el contador sea mayor que el último aceptado: así rechaza URLs falsificadas y repetidas.
- Funciona con la lectura NFC nativa de Android y de iPhone reciente (sin app).
- El contador es de 24 bits (unos 16 millones de lecturas), suficiente para una mesa.

### Claves ([ADR 0011](adr/0011-claves-nfc.md))
- Cada sticker tiene una **clave derivada** de la clave maestra del restaurante y del UID del sticker.
- La **clave maestra** es una por restaurante y vive en un servicio de gestión de claves (KMS) que nunca la deja salir.
- Nunca se versionan ni se escriben en documentos.

### Programación (la hace Hungría antes de entregar)
1. Activar SDM: viene **apagado** de fábrica.
2. Definir el formato de la URL y qué campos se incluyen (UID, contador, firma).
3. **Cambiar las claves de fábrica** (vienen en ceros) por la clave derivada del sticker.
4. Comprobar la lectura con un teléfono y asociar el sticker a su mesa en el Núcleo.
5. Enviar al restaurante, que lo pega en la mesa. Comprar a un distribuidor fiable: hay clones sin SDM real, y "NTAG 424" sin "DNA" no existe como producto.

### Reposición
Si un sticker se daña, se pierde o lo despegan, el encargado lo **desactiva** en el Núcleo y se pide un reemplazo. Mientras llega, la mesa funciona con su QR. Un sticker desactivado se rechaza aunque su firma sea válida. No hay rotación periódica de claves.

## Secuencia de apertura
```mermaid
sequenceDiagram
    participant C as Cliente
    participant T as Sticker NFC / QR
    participant S as Servidor
    C->>T: toca o escanea
    T-->>C: URL (NFC: con UID, contador y firma)
    C->>S: abre la URL
    alt NFC válido y contador mayor al último
        S-->>C: sesión de mesa abierta o unirse
    else NFC inválido o repetido
        S-->>C: rechazar y ofrecer llamar al mesero
    else QR
        S-->>C: sesión abierta; pedir requiere confirmación
    end
```

## Límites de seguridad
- La URL del toque **solo sirve para abrir o unirse**. La sesión ya abierta se protege con su propio token.
- Cada comensal que entra recibe un nombre de animal; **vincular invitados es explícito** (ver [sesión de mesa](sesion-de-mesa.md)).
- El mesero puede expulsar a un participante.

## Qué hacer si falla
- Sticker dañado o sin lectura: usar el QR o pedir al mesero (vía humana siempre disponible).
- Sin red: la validación NFC depende del servidor; si cae, el flujo pasa a pedido con el mesero ([ADR 0006](adr/0006-operacion-sin-red.md)).
