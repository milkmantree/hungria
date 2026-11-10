# ADR 0010 — Eventos y comandos entre módulos

- Fecha: 2026-11-09
- Estado: aceptado

## Contexto
Los módulos se activan por local según la licencia ([ADR 0009](0009-licencias-y-activacion-de-modulos.md)) y se comunican solo por contratos ([ADR 0001](0001-modularidad.md)). Hacía falta fijar cómo se comunican, de forma que funcione aunque un módulo no esté activo y con una red inestable.

## Decisión
- **Dos tipos de mensaje:**
  - **Evento:** "pasó algo". Lo publica el módulo dueño del dato; puede no tener a nadie escuchando y nadie responde.
  - **Comando:** "haz esto", dirigido a un módulo concreto, que responde con el resultado. Solo se envía a módulos **activos** en el local; si no lo están, quien lo envía aplica la degradación de [dependencias](../plataforma/dependencias.md).
- **Nombres en inglés** con la forma `modulo.entidad.verbo`, en minúsculas y con `snake_case` dentro de cada parte. Eventos con el verbo en pasado (`floor.session.opened`); comandos en imperativo (`payments.charge.create`).
- **Datos mínimos:** los eventos llevan IDs y datos clave (local, mesa, grupo, montos, estados). Quien necesite más lo consulta al módulo dueño. **Los datos personales** (correo, RUC, nombre) no viajan en eventos; solo en los comandos que los necesitan.
- **Entrega al menos una vez:** cada mensaje tiene un ID único y el receptor ignora los que ya procesó. Los reintentos son seguros.
- **Versión en cada mensaje.** Los cambios compatibles (agregar campos opcionales) no cambian la versión; los incompatibles crean una versión nueva y la anterior se mantiene un tiempo.

Catálogo: [eventos y comandos](../plataforma/eventos.md).

## Consecuencias
- Un módulo nunca falla porque otro no esté activo: los eventos se publican igual y los comandos se evitan según la licencia.
- Cobros y comprobantes se siguen paso a paso porque son comandos con respuesta.
- Cada receptor debe guardar qué IDs ya procesó.
- La auditoría y las automatizaciones del Núcleo escuchan todos los eventos.
