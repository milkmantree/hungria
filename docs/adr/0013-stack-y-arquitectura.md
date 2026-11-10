# ADR 0013 — Stack y arquitectura del backend

- Fecha: 2026-11-10
- Estado: aceptado (frontend pendiente)

## Contexto
Termina el diseño de la fase 1 y se pasa a código. Faltaba elegir lenguaje, framework, base de datos, mecanismo de eventos y hosting. Las restricciones vienen de ADRs anteriores:
- Módulos independientes con contratos ([ADR 0001](0001-modularidad.md)), activados por local según la licencia ([ADR 0009](0009-licencias-y-activacion-de-modulos.md)).
- Eventos y comandos con entrega al menos una vez e idempotencia ([ADR 0010](0010-eventos-y-comandos.md)).
- Claves NFC en un KMS en la nube que nunca las deja salir ([ADR 0011](0011-claves-nfc.md)).
- Experiencia en vivo en la mesa: grupos, estados de pedidos y llamados al mesero en tiempo real.
- Equipo de dos personas: pocas piezas que operar.

## Decisión
**Lenguaje y framework**
- **Python** con **Django** y **Django Channels** (WebSockets para el tiempo real).
- **Monolito modular:** un solo despliegue y una app de Django por módulo. Los nombres de las apps son los prefijos de los eventos: `core` (Núcleo), `floor` (Sala), `kitchen` (Cocina), `tableside` (Mesa digital), `payments` (Pagos), `reception` (Recepción y reservas), y así con los siguientes.
- Una app **no importa modelos ni código interno de otra**. Se comunica solo por su API pública (comandos) y por eventos. La regla se verifica en CI con un linter de imports (por ejemplo, import-linter).
- **Back-office:** el admin de Django al inicio.

**Datos y eventos**
- **PostgreSQL** como base de datos única. Cada app es dueña de sus tablas.
- **Outbox transaccional:** el evento se guarda en la misma transacción que el cambio que lo origina y se publica después. Así no hay eventos perdidos ni eventos de cambios que no ocurrieron.
- **Cola de tareas con procrastinate**, sobre el mismo Postgres: publica el outbox, reintenta cobros y comprobantes, y corre los temporizadores (vencimientos, inactividad, escalamiento de llamados).
- Cada receptor registra los IDs de mensaje que ya procesó ([ADR 0010](0010-eventos-y-comandos.md)).
- **Redis** solo como canal de Channels para los WebSockets, nunca como fuente de verdad.
- **Dinero en céntimos** (enteros), como fija el [módulo Pagos](../modulos/pagos/README.md).

**Infraestructura**
- **Contenedores Docker.** El mismo contenedor corre en local y en la nube.
- **Google Cloud, región Santiago (`southamerica-west1`)**, la más cercana a Perú con los servicios necesarios:
  - **Cloud Run** para la web, los WebSockets y los workers de procrastinate.
  - **Cloud SQL** para PostgreSQL.
  - **Memorystore** para Redis.
  - **Cloud KMS** para las claves maestras NFC ([ADR 0011](0011-claves-nfc.md)).
  - **Secret Manager** para credenciales de pasarelas y PSE/OSE. Nunca en el repo.
- Ambientes: local (Docker Compose), staging y producción.

**Frontend**
- **Pendiente.** Las PWA del cliente (Mesa digital) y del mesero (Sala) se deciden después, junto con el sistema de diseño. El backend expone una API JSON y WebSockets, así que no depende de esa elección.

## Consecuencias
- Una sola base de código y un solo despliegue. Separar un módulo en su propio servicio más adelante es posible, porque ya se comunica solo por contratos.
- Postgres concentra datos, outbox y cola: menos piezas, pero es punto único de falla. Cloud SQL con alta disponibilidad en producción.
- Los datos quedan en Chile. Hay que revisar los requisitos de **transferencia internacional** de la Ley 29733 antes del piloto (ver [preguntas abiertas](../preguntas-abiertas.md)).
- Primer corte de código: Núcleo, Sala y Mesa digital en modo Acompañado. Pagos arranca con una pasarela simulada (`FakeGateway`) hasta conocer la del piloto.
