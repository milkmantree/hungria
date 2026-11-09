# Comparativa con TastyIgniter

Revisión del 2026-11-09 de los 31 repositorios de la organización [tastyigniter](https://github.com/orgs/tastyigniter/repositories?type=all), tomado como referencia de arquitectura ([ADR 0009](adr/0009-licencias-y-activacion-de-modulos.md)). Fuente: los README de cada repositorio. No se reutiliza su código.

## Qué es cada repositorio
| Repositorio | Qué hace | Equivalente en Hungría |
|---|---|---|
| core, ti-module-admin/main/system | Núcleo, panel de administración, sistema de extensiones | Núcleo |
| ti-ext-cart | Carrito y pedidos online: delivery y para llevar, propinas e impuestos, cartas por horario, checkout de una página, aceptar o rechazar pedidos | Sala y Mesa digital (solo en mesa) |
| ti-ext-payregister | Pasarelas (Stripe, PayPal, Square, Mollie, Authorize.net, pago contra entrega), perfiles de pago guardados, reembolsos | Pagos y comprobantes |
| ti-ext-reservation | Reservas online, asignación automática de mesa, tiempos de estadía y anticipación, correos de confirmación, áreas del salón | Recepción y reservas (solo lista de espera) |
| ti-ext-local | Varios locales, zonas de reparto con costo, horarios de atención, reseñas por local, buscar local cercano | Núcleo (locales), parcial |
| ti-ext-coupons | Cupones fijos y porcentuales, por local, por horario, con monto mínimo | No existe |
| ti-ext-automation | Reglas "cuando pase X, haz Y" con condiciones, en segundo plano | Núcleo (automatizaciones) |
| ti-ext-broadcast | Notificaciones en tiempo real en el navegador | Avisos al mesero, sin canal definido |
| ti-ext-user | Clientes y personal, registro con verificación de correo, recuperar contraseña, suplantar usuarios para soporte | Núcleo (personal) y Cuenta de cliente (futuro) |
| ti-ext-socialite | Inicio de sesión con Google, Facebook y otros | No existe |
| ti-ext-translate | Contenido y carta en varios idiomas, selector de idioma | Núcleo (carta bilingüe) |
| ti-ext-api | API REST con tokens para todos los recursos | Solo eventos internos y adaptador de caja |
| ti-ext-frontend, ti-ext-pages, storefront, ti-theme-orange | Sitio web del restaurante: páginas, menús, banners, slider, newsletter, contacto, reCAPTCHA, temas | No existe |
| setup | Asistente de instalación | No aplica (Hungría es un servicio, no se instala) |
| ti-ext-demo, ti-ext-debugbar, ti-ext-dusk, flame, workflows, docs, .github | Demo, depuración, pruebas, librería base, CI, documentación | Ingeniería, fase de código |
| ti-ext-drivers, ti-ext-eventrules, ti-ext-onlinetracker | Archivados | — |

## Qué le falta a Hungría
| # | Función en TastyIgniter | Situación en Hungría |
|---|---|---|
| F1 | **Para llevar y delivery**, con zonas y costo de reparto | Solo servicio en mesa |
| F2 | **Pedidos online desde el sitio web** del restaurante | Solo PWA en la mesa |
| F3 | **Reservas online** completas | Recepción y reservas solo tiene lista de espera |
| F4 | **Horarios de atención y cartas por horario** (desayuno, almuerzo, cena) | La carta no tiene horarios |
| F5 | **Opciones de plato** (tamaño, punto, extras con precio) | La carta no tiene opciones ni extras |
| F6 | **Cupones, descuentos y promociones** | Solo se mencionan cortesías resueltas por una persona |
| F7 | **Reseñas públicas** por local | Solo feedback privado |
| F8 | **Cuenta de cliente**: registro, recuperar contraseña, login social, tarjeta guardada | Cuenta de cliente es futuro y sin detalle |
| F9 | **Notificaciones**: plantillas de correo y avisos en tiempo real | Solo se dice "avisar", sin canal ni plantillas |
| F10 | **API pública** con tokens para terceros | Solo eventos internos |
| F11 | **Impuestos y cargos** configurables | No está definido cómo se muestran el IGV ni el recargo al consumo |
| F12 | **Panel de administración** con indicadores | Solo reportes básicos de ventas |
| F13 | **Suplantar usuarios** para dar soporte | No definido |
| F14 | **Sitio web** del restaurante (páginas, temas) | No existe |

## Qué está mejor en Hungría
| Tema | Hungría | TastyIgniter |
|---|---|---|
| Servicio en mesa | Sesión de mesa con grupos, invitados y cuentas separadas por grupo | El núcleo oficial no tiene pedido en mesa; existe una extensión de terceros (Thoughtco Dine-in) |
| Acceso a la mesa | NFC con firma y contador (prueba de presencia), QR de respaldo | No aplica |
| Atención humana | Modos Directo y Acompañado; alergias siempre revisadas por una persona; vía humana en cada paso | Pensado para autoservicio online |
| Operación del mesero | Módulo Sala: confirmar, editar, mover ítems, pagos por fuera, fusionar mesas | Panel de administración, no una app de sala |
| Cocina | Estados por plato, pantalla e impresora, alertas de demora | Estados por pedido; sin pantalla de cocina oficial |
| Llamados | Llamado con motivo y escalado al encargado | No existe |
| Pagos en Perú | Pasarela propia del restaurante con adaptadores (Culqi, Izipay, Niubiz…), Yape y Plin | Pasarelas internacionales; ninguna peruana |
| Comprobantes | Boleta y factura SUNAT vía PSE/OSE | No existe |
| Dinero | Saldo a favor y reembolso automático al cierre; propina por grupo | Reembolsos manuales por intento de pago |
| Integración | Envío de ventas al sistema de caja | No existe |
| Sin red | Degradación documentada (4G, papel, reconciliación) | No definido |
| Modelo comercial | Licencia por local, paquetes y módulos extra | Código abierto que cada restaurante instala |
| Privacidad | Sesión anónima, datos mínimos, Ley 29733 | Cuenta de cliente tradicional |

## Cuestionario
Cada pendiente se decidió con preguntas, como en las sesiones anteriores. Las respuestas están en el [ADR 0012](adr/0012-alcance-frente-a-tastyigniter.md).

| # | Pregunta | Estado |
|---|---|---|
| F5 | ¿La carta tiene opciones de plato y extras con precio? | decidido: opciones y extras en el Núcleo |
| F11 | ¿Cómo se muestran el IGV y el recargo al consumo? | decidido: IGV incluido, sin recargo |
| F4 | ¿La carta tiene horarios? | decidido: cartas por horario en el Núcleo |
| F6 | ¿Hay cupones, descuentos o cortesías? ¿Quién los autoriza? | decidido: cortesías, descuentos del mesero, módulo Cupones |
| F1 | ¿Se incluye para llevar o delivery? ¿Integración con apps de delivery? | decidido: Para llevar y Delivery por apps; sin delivery propio |
| F2, F14 | ¿Pedidos online y sitio web del restaurante? | decidido: solo enlace a la PWA, sin sitio |
| F3 | ¿Reservas online? ¿Cuándo? | decidido: fase 1 |
| F7 | ¿Reseñas públicas o solo feedback privado? | decidido: feedback privado e invitación a Google |
| F8 | ¿Qué incluye la cuenta de cliente? | decidido: correo, Google o Apple, tarjeta guardada, historial |
| F9 | ¿Por qué canales se notifica (correo, WhatsApp, push)? | decidido: correo y SMS |
| F10 | ¿API pública para terceros? | decidido: no por ahora |
| F12 | ¿Panel con indicadores? ¿Reportes avanzados como módulo? | decidido: módulo Reportes avanzados |
| F13 | ¿Suplantación de usuarios para soporte? | decidido: sí, autorizado y auditado |
