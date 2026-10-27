# Visión

## Objetivo a largo plazo
Ofrecer herramientas digitales y de IoT para gestionar un restaurante de punta a punta, construidas como módulos independientes que se pueden adoptar por separado y componer entre sí.

## Propuesta de valor
Apalancar la tecnología lo máximo posible **sin poner en jaque la calidad de la atención**. Medimos la tecnología por el tiempo y la atención que devuelve al personal para el trato humano, no por cuánto reemplaza.

## Primer caso: restaurante casual
Restaurante casual de 10 a 20 mesas. Cada mesa tiene un sticker NFC y un QR propios para abrir una **sesión de mesa** en el celular del cliente. El restaurante elige entre dos [modos de servicio](modos-de-servicio.md): **Directo** (autonomía, pago por adelantado) o **Acompañado** (el mesero confirma, pago al final).

## Alcance por fases
| Fase | Foco | Estado |
|---|---|---|
| 1 | Flujos de atención al cliente (diseño) | en curso |
| 2+ | Módulos: pagos, cocina, personal, inventario, cuenta de cliente | planeado |

## Fase 1: alcance
- Definir el modelo de [sesión de mesa](sesion-de-mesa.md) con grupos y el [acceso por NFC/QR](acceso-a-la-mesa.md).
- Mapear el recorrido del cliente (llegada y acceso, pedido, servicio, cuenta y pago, cierre y comprobantes).
- Definir, en cada paso, qué hace la tecnología y dónde el humano es obligatorio.
- Derivar requisitos y contratos del módulo de atención al cliente.

## Futuro registrado
Historial de visitas y acumulador de boletas en la interfaz del cliente (módulo Cuenta de cliente). No se diseña en esta fase.

## No-objetivos (por ahora)
- Escribir código o elegir hardware más allá del sticker NFC.
- Diseñar a detalle cocina, personal o inventario (solo sus contratos con atención al cliente).
- Sustituir al personal de sala.
