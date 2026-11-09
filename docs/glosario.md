# Glosario

| Término | Definición |
|---|---|
| Comensal | Persona que consume en el restaurante. |
| Mesa | Unidad física de servicio; puede unirse o dividirse. |
| Sesión de mesa | Contenedor digital de todo lo que ocurre en una mesa; se abre con NFC o QR. Ver [sesión de mesa](sesion-de-mesa.md). |
| Grupo | Titular más invitados vinculados, con cuenta y pago propios. Un comensal solo es un grupo de uno. |
| Titular | Comensal que arma el pedido del grupo y paga por él. |
| Invitado vinculado | Comensal que el titular aceptó explícitamente en su grupo. |
| Nombre de animal | Identidad anónima y visible de cada usuario en la sesión (gato, ballena...). |
| Modo Directo | Modo de servicio donde el pago confirma el pedido y lo envía a cocina. |
| Modo Acompañado | Modo de servicio donde el mesero confirma el pedido y el pago es al final. |
| PWA | Aplicación web que se abre desde el navegador sin instalar nada; es la interfaz del cliente. |
| Saldo a favor | Monto ya pagado por un grupo que quedó sin usar tras una cancelación o edición; se aplica a sus siguientes pedidos o se reembolsa al cerrar. |
| Pasarela de pagos | Servicio que procesa los pagos digitales (tarjetas, Yape, Plin, Apple Pay, Google Pay). Cada restaurante conecta la suya por API. |
| PSE / OSE | Proveedor autorizado por SUNAT que emite y valida comprobantes electrónicos. |
| RUC | Registro Único de Contribuyentes de Perú; necesario para emitir factura. |
| Sistema de caja | Software POS del restaurante que lleva ventas, caja y contabilidad. Hungría le envía las ventas liquidadas. Distinto del terminal POS físico de tarjetas. |
| KDS | Pantalla de cocina que muestra las comandas y el estado de cada plato. |
| Pago por fuera | Pago por un medio externo (POS, efectivo) que el mesero registra en el sistema. |
| NFC / SDM | Sticker NFC que genera una URL única y firmada en cada lectura (Secure Dynamic Messaging). Ver [acceso a la mesa](acceso-a-la-mesa.md). |
| Comanda | Pedido enviado a cocina/barra, con ítems, notas y alergias. |
| Ítem | Producto del menú dentro de un pedido. |
| Plato compartido | Ítem pedido para varios, cargado a un solo grupo. |
| Cuenta | Total consumido por un grupo. |
| Comprobante | Boleta (por defecto) o factura (con RUC) electrónica de SUNAT, emitida por grupo al liquidarse. |
| Lista de espera | Cola de grupos sin mesa asignada. |
| Turno | Periodo de trabajo del personal; también franja de servicio. |
| Sala | Zona de atención al cliente (frente de casa). |
| Cocina | Zona de preparación (parte trasera). |
| Vía humana | Alternativa atendida por una persona a cualquier paso digital. |
| Degradación elegante | Continuar operando con medios manuales cuando falla la tecnología. |
| Módulo | Unidad funcional independiente de Hungría con contratos explícitos; se activa por local según la licencia. |
| Núcleo | Base siempre activa: restaurante y locales, mesas y zonas, carta, usuarios y roles, licencia, reportes básicos, auditoría y automatizaciones. |
| Licencia | Conjunto de módulos activos en un local. |
| Paquete | Combinación base de módulos que se vende junta (Mesero, Mesero con cobro, Mesa digital, Completo). |
| Módulo extra | Módulo que se suma a un paquete, si cumple sus dependencias. |
| Sala | Módulo de operación del mesero. |
| Mesa digital | Módulo de autoservicio del cliente en la mesa (PWA, NFC/QR). |
| Recepción y reservas | Módulo de lista de espera y, más adelante, reservas. |
| Contrato | Interfaz (eventos/datos) que un módulo expone o consume. |
