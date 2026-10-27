# Principios de diseño

1. **La tecnología quita fricción, no calidez.** Automatizar esperas, errores de comanda y cobro; nunca el saludo, la recomendación ni la resolución de un problema.
2. **Siempre hay una vía humana.** Todo paso digital tiene alternativa atendida por una persona, sin penalización para el cliente.
3. **El humano decide en lo sensible.** Alergias, quejas, excepciones y cortesías las resuelve una persona; el sistema avisa y prepara contexto.
4. **Degradación elegante.** Si cae la red o un dispositivo, el servicio continúa (comanda en papel, cobro manual) y se reconcilia después.
5. **Invisible cuando funciona.** El cliente no debería tener que aprender nada; el personal ve lo que necesita en el momento justo.
6. **El personal es usuario de primera clase.** Cada flujo se diseña también para quien sirve; si les estorba, está mal.
7. **Modular y con contratos.** Cada módulo expone y consume interfaces explícitas; ninguno depende de los internos de otro (ver [ADR 0001](adr/0001-modularidad.md)).
8. **Datos mínimos.** Se recoge solo lo necesario, con consentimiento claro para datos del cliente.
9. **Medible.** Cada flujo define métricas de calidad (tiempos, errores, satisfacción) para saber si la tecnología ayuda.

## Prueba de decisión
Antes de automatizar un paso: ¿libera tiempo del personal para atender mejor? ¿el cliente puede optar por un humano? ¿qué pasa si falla? Si alguna respuesta es mala, se rediseña.
