# PE 90.1 · Propuesta de prevención y concienciación para Logisticfy

## 1. Marco de protección

### 1.1. Análisis del contexto y necesidades de protección

**Hechos del caso.** Logisticfy presta servicios de gestión logística B2B desde Barcelona. Unos 25 clientes empresariales generan entre 80 y 120 expediciones al día. Tres transportistas externos realizan el transporte físico. La plantilla tiene 20 personas, incluida una en prácticas en IT. Una expedición nace en el portal, Operaciones valida la solicitud y asigna transportista, el seguimiento alimenta la atención al cliente y Administración utiliza la información para facturar. Un estado incorrecto puede afectar a las tres áreas. Las direcciones de entrega y los contactos pueden identificar a personas.

**Criterio de selección.** Se utilizan los identificadores del inventario corporativo para justificar medidas sobre los puestos y el flujo de expediciones. Las necesidades de protección y las medidas de los apartados siguientes son propuestas.

| ID&nbsp;del&nbsp;activo | Activo | Necesidad de protección | Proceso o función relacionada |
|---|---|---|---|
| SW-&#8288;01 | Plataforma web y backoffice | Mantener el acceso a las expediciones y limitar cambios a perfiles autorizados. Un cambio incorrecto puede propagarse a atención y facturación. | Alta, validación, seguimiento y gestión de incidencias. |
| DAT-&#8288;01 | Base de datos de clientes, envíos y facturación | Restringir la consulta de datos personales y conservar la exactitud de estados e importes. | Operaciones, Atención y Administración. |
| SW-&#8288;02&nbsp;/&nbsp;EXT-&#8288;01 | API propia e integraciones con tres transportistas | Distinguir el dato recibido por la integración del recibido por correo y comprobar el origen antes de aplicar cambios. Enviar a cada proveedor solo los datos necesarios. | Asignación y seguimiento. SW-02 es el componente propio y EXT-01 la dependencia externa. |
| IAM-&#8288;01 | Identidades y mecanismos de acceso | Identificar al responsable de cada acción y limitar permisos por cometido y duración. | Backoffice, facturación y administración técnica. |
| HW-&#8288;01&nbsp;/&nbsp;PHY-&#8288;01 | Puestos Windows, oficina y equipos compartidos | Proteger sesiones abiertas, dispositivos y documentación impresa frente a accesos ajenos. | Trabajo diario, visitas y cambios de turno. |
| COM-&#8288;01 | Correo corporativo | Evitar que peticiones suplantadas o errores de destinatario provoquen cambios indebidos o divulgación. | Coordinación con clientes y transportistas. |
| MON-&#8288;01 | Registros y monitorización | Conservar evidencia suficiente para revisar cambios de permisos y anomalías sin copiar información innecesaria. | Soporte e investigación interna. |
| BKP-&#8288;01 | Copias de seguridad | Poder recuperar información utilizable y preservar las copias frente a accesos o alteraciones. | Reanudación de la gestión y facturación tras una interrupción. |

### 1.2. Principios generales de ciberseguridad

| ID | Principio propuesto | Aplicación en Logisticfy | Justificación |
|---|---|---|---|
| P-&#8288;01 | Mínimo privilegio y responsabilidad individual | Asignar accesos según función y utilizar identidades personales. | Consultar una incidencia, cambiar una ruta y administrar permisos son tareas distintas (IAM-01, SW-01). Fundamenta N-01 y N-02. |
| P-&#8288;02 | Integridad y trazabilidad de las operaciones | Confirmar por un canal conocido los cambios sensibles y registrar su origen. | Los cambios de destino o proveedor afectan al envío, la atención y la facturación (DAT-01, COM-01, EXT-01). Fundamenta N-05. |
| P-&#8288;03 | Confidencialidad y datos necesarios | Limitar los datos compartidos, sus destinatarios y los lugares donde se guardan. | El transporte puede requerir una dirección, pero normalmente no los datos de otras expediciones o de facturación (DAT-01, COM-01). Fundamenta N-04 y N-06. |
| P-&#8288;04 | Continuidad y recuperación comprobable | Mantener puestos gestionados y preparar pruebas de restauración aisladas. | La interrupción del acceso a las expediciones afecta simultáneamente a varias áreas (HW-01, SW-01, BKP-01). Fundamenta N-03 y N-08. |
| P-&#8288;05 | Detección y aviso temprano | Facilitar la comunicación de anomalías y el manejo seguro de las evidencias. | Un aviso a tiempo puede frenar un cambio indebido y ayudar a reconstruir qué ocurrió (MON-01, COM-01). Fundamenta N-07. |

**Conocimiento y respaldo de Dirección.** El responsable IT presentaría al CEO y al responsable de operaciones un resumen de una página con ejemplos de cambio de destino, pérdida de equipo e interrupción del portal. En una reunión de 30 minutos se acordarían prioridades, responsables, recursos iniciales y calendario. Dirección dejaría constancia del respaldo y de cualquier condición en un acta vinculada a la versión de la normativa. Tras la aprobación, IT publicaría la versión vigente en el espacio corporativo acordado y cada responsable explicaría a su equipo qué cambia y registraría la recepción.

### 1.3. Normativa de protección del puesto de trabajo

**Ámbito.** Las 20 personas que emplean datos, sistemas o espacios corporativos, incluida la persona en prácticas. Las reglas se aplican según funciones y nivel de acceso. El manejo de datos con transportistas afecta al personal que interactúa con ellos.

**Responsabilidades.** Dirección patrocina la norma y autoriza excepciones que impliquen riesgo residual. Los responsables de área justifican accesos y supervisan la aplicación. IT mantiene los controles, revisa evidencias y recibe avisos. Cada trabajador aplica las reglas y comunica anomalías. El tutor de prácticas revisa las tareas y solicita el cierre de accesos al terminar la asignación.

| ID | Norma propuesta | Destinatarios | Aplicación y posible verificación | Excepciones, si procede |
|---|---|---|---|---|
| N-&#8288;01 | Usar cuenta individual, activar MFA cuando esté habilitado y rechazar peticiones de autenticación inesperadas. | Toda la plantilla. | IT cotejaría cuentas con el listado de personal y comprobaría la configuración de MFA en los servicios que lo permitan. | Si una plataforma no admite MFA, IT registra el caso y propone un control compensatorio con fecha de revisión. |
| N-&#8288;02 | Solicitar permisos por tarea y fecha de fin. Utilizar una cuenta administrativa separada para tareas privilegiadas. La persona en prácticas trabajará con datos ficticios en pruebas y con tutor asignado. | Responsables de área, IT y personal en prácticas. | El responsable solicita, IT concede y registra la caducidad. Se revisan accesos al cambiar de función y se revocan al finalizar la relación. Revisar tickets frente a permisos efectivos. | Para una intervención urgente, permiso temporal al personal autorizado con tarea, vencimiento y revisión posterior. |
| N-&#8288;03 | Usar equipos corporativos y aplicaciones aprobadas. Bloquear el equipo al levantarse e instalar actualizaciones según indique IT. | Toda la plantilla e IT. | IT mantendría el catálogo y el estado de actualizaciones. Una muestra de equipos permitiría comprobar bloqueo y software. | Aplicación excepcional aprobada por IT para una tarea concreta, con plazo y retirada. |
| N-&#8288;04 | Tratar expediciones y facturas en herramientas corporativas. Antes de compartir, comprobar destinatario y limitar los campos a los necesarios. | Operaciones, Atención, Comercial y Administración. | Consultar el sistema autorizado, evitar nubes y correos personales, y registrar los intercambios excepcionales. Revisar muestras con metadatos o datos ficticios. | Exportación autorizada con motivo, destinatario, ubicación protegida y fecha de retirada. |
| N-&#8288;05 | Antes de cambiar destino, transportista o datos de cobro a raíz de un mensaje, contrastar por un contacto corporativo conocido y registrar la validación. | Operaciones, Atención y Administración. | No verificar con el teléfono o enlace del propio mensaje. Si no se confirma, mantener el cambio pendiente y avisar por N-07. Revisar una muestra de cambios y su registro. | La urgencia se escala al responsable. La confirmación independiente se mantiene. |
| N-&#8288;06 | Acompañar a las visitas en zonas de trabajo, proteger impresos y retirar documentación de zonas y equipos compartidos al terminar. | Toda la plantilla y responsables de oficina. | Custodiar documentación en la ubicación prevista y usar destrucción segura de copias que ya no se necesiten. Revisar registro de visitas y una muestra de zonas al cierre. | Acceso de mantenimiento autorizado y acompañado. |
| N-&#8288;07 | Ante mensaje sospechoso, pérdida de equipo o autenticación no solicitada, avisar de inmediato a IT. Indicar hora, canal, referencia y qué se hizo. | Toda la plantilla. | Usar el canal corporativo acordado con IT. Si el equipo o correo está afectado, llamar al contacto interno conocido. Conservar el mensaje original y evitar copiar datos personales innecesarios. Revisar registros de avisos y tiempos. | La falta de acceso al canal se cubre con la alternativa telefónica. |
| N-&#8288;08 | Comprobar que las copias de expediciones y facturación pueden restaurarse en un entorno aislado, con acceso limitado. | IT y responsables de Operaciones y Administración. | IT propone una prueba trimestral, verifica con las áreas una muestra restaurada y registra alcance, tiempo y correcciones. | Si se aplaza, registrar causa y fecha de reemplazo aprobada por IT y Dirección. |

**Comunicación y revisión.** IT distribuiría la versión aprobada en las reuniones de equipo y en la incorporación. Se propone revisar la norma cada seis meses y tras cambios importantes de sistema, proveedor o proceso, o tras un incidente relevante. Las excepciones se registrarían con motivo, alcance, responsable, control compensatorio, aprobación, vencimiento y retirada. El responsable IT revisaría las abiertas mensualmente. Las verificaciones descritas son mecanismos previstos para una revisión posterior.

## 2. Programa de concienciación

### 2.1. Objetivos y destinatarios

| ID | Objetivo de concienciación | Destinatarios | Justificación |
|---|---|---|---|
| O-&#8288;01 | Detener una petición sospechosa de cambio de destino, confirmar por un canal independiente y avisar si no se valida. | Operaciones y Atención al Cliente, 10 personas. | Son los equipos que gestionan expediciones y reciben consultas. Refuerza N-05 y N-07. |
| O-&#8288;02 | Identificar y comunicar una petición MFA inesperada, y solicitar permisos con alcance y vencimiento. | Toda la plantilla. IT y la persona en prácticas practican además la solicitud temporal con tutor. | Los permisos afectan a todos los puestos, con atención especial a los accesos técnicos. Refuerza N-01, N-02 y N-07. |
| O-&#8288;03 | Compartir una expedición ficticia con el destinatario correcto, los campos imprescindibles y una herramienta autorizada. | Operaciones, Atención y Administración, 12 personas. | Usan el mismo dato en distintos momentos y pueden necesitar campos diferentes. Refuerza N-04 y N-06. |

### 2.2. Plan de acciones de concienciación

| ID | Objetivo | Destinatarios | Acción y canal | Temporalización | Responsable | Material |
|---|---|---|---|---|---|---|
| A-&#8288;01 | O-01 | Operaciones y Atención | Microtaller presencial con un caso ficticio y práctica de un aviso. | Semana 1, 15 min en dos turnos para mantener el servicio. Refuerzo en semana 4. | Coordinador logístico con apoyo de IT y responsable de Atención. | M-01, ficha incluida en 3.1. |
| A-&#8288;02 | O-02 | Toda la plantilla | Demostración breve de alertas MFA con ejemplos estáticos. IT añade una práctica de solicitud de acceso temporal con el tutor. | Semana 2, 12 min, más 10 min para perfiles técnicos. Incorporaciones durante su primera semana. | Responsable IT y tutor de prácticas. | M-02, capturas ficticias y modelo de solicitud, previstos. |
| A-&#8288;03 | O-03 | Operaciones, Atención y Administración | Dos ejemplos contrastados en reunión de área. Cada persona selecciona canal, destinatario y campos a compartir. | Semana 3, 15 min. Variante de repaso en semana 5. | Responsables de área con revisión de IT. | M-03, casos ficticios y lista de comprobación, previstos. |

### 2.3. Seguimiento y evaluación

| Objetivo&nbsp;o&nbsp;acción | Indicador y meta inicial | Evidencia prevista | Momento de revisión |
|---|---|---|---|
| O-&#8288;01&nbsp;/&nbsp;A-&#8288;01 | Al menos 9 de 10 convocados resuelven correctamente las tres decisiones del caso: parar, verificar fuera del mensaje y avisar. Registrar participación por separado. | Respuesta individual al caso y ejercicio de aviso evaluados con la clave de M-01, con recuento agregado. | Semana 1 y nuevo caso de dificultad similar en semana 4. |
| O-&#8288;02&nbsp;/&nbsp;A-&#8288;02 | Al menos 18 de 20 convocados rechazan y notifican la petición MFA ficticia. En el subgrupo técnico, comprobar por separado que cada solicitud de práctica incluye alcance y caducidad. | Recuento de respuestas y lista de comprobación de solicitudes ficticias. | Semana 2 y un mes después. |
| O-&#8288;03&nbsp;/&nbsp;A-&#8288;03 | Al menos 11 de 12 convocados aciertan destinatario, canal y datos necesarios en un escenario nuevo. | Hoja de casos con respuestas y recuento agregado de errores por criterio. | Semana 3 y repaso en semana 5. |

**Revisión y mejora.** Los recuentos usan como denominador las personas convocadas. Las ausencias se registran aparte para programar recuperación. IT y los responsables de área revisarían qué paso provoca más errores. Por ejemplo, si el equipo elige un teléfono incluido en el mensaje, se repetiría el ejercicio con dos contactos y se mostraría cómo encontrar el contacto registrado. El siguiente caso mediría la misma conducta con otra situación. Las metas son propuestas, pendientes de contrastar con las primeras mediciones. Los resultados se comunicarían en agregado y servirían para ajustar formación y materiales.

## 3. Desarrollo del material de concienciación

### 3.1. Material desarrollado

- **ID:** M-01.
- **Título:** Antes de cambiar un destino, para y verifica.
- **Formato:** ficha textual con caso ficticio, ejercicio, ejemplo de aviso y clave de corrección.
#### M-01 · Antes de cambiar un destino, para y verifica

**Logisticfy · Operaciones y Atención al Cliente · Microtaller de 15 minutos**

Acción A-01 · Objetivo O-01 · Normas N-05 y N-07

Un cambio de dirección afecta a dónde acaba el paquete. Una petición urgente puede ser legítima y aun así necesita confirmación.

1. **Para.** Deja la expedición sin cambiar. Evita abrir enlaces o adjuntos inesperados y no respondas con direcciones, cuentas o documentos.
2. **Verifica.** Abre el backoffice desde tu acceso habitual. Contrasta la solicitud con tu responsable o con un contacto del cliente o transportista que ya conste en el directorio corporativo. Si se confirma, que el perfil autorizado registre quién confirmó, cuándo y qué cambió.
3. **Avisa.** Si el contacto no confirma el cambio, el mensaje resulta sospechoso o ya interactuaste con él, escala a IT. Conserva el original y cuenta qué hiciste. Si el correo o equipo está afectado, utiliza el contacto telefónico interno conocido.

##### Caso para resolver en cinco minutos

A las 10:15 recibes un mensaje atribuido a un transportista. Pide cambiar hoy mismo el destino de la expedición ficticia **LF-DEMO-027**. Ofrece un teléfono alternativo y un adjunto con la supuesta dirección nueva. El backoffice no muestra una solicitud de cambio. Los datos del ejercicio son ficticios y no hay enlaces ni adjuntos activos.

Escribe tres respuestas breves:

1. ¿Qué haces con la expedición y el adjunto inmediatamente?
2. ¿Dónde encuentras el contacto con el que comprobarías la petición?
3. Si el contacto oficial no confirma el cambio, ¿a quién avisas y qué incluyes?

##### Práctica de aviso

> **Asunto:** Solicitud de cambio sin confirmar · LF-DEMO-027

> **Hora y canal:** 10:15, correo corporativo.

> **Hecho observado:** se pide cambiar destino y usar un contacto alternativo. El contacto registrado no confirma la solicitud.

> **Acciones realizadas:** no se cambió el destino. No se abrió el adjunto. El original está conservado.

> **Ayuda solicitada:** revisión por IT y registro del aviso.

El ejemplo se completa con lo que haya ocurrido de verdad. Si abriste un adjunto o facilitaste un dato, inclúyelo en el aviso sin reproducir el dato sensible.

##### Corrección para el facilitador

Da un punto por cada decisión correcta: **(1)** mantener el destino y no abrir el adjunto, **(2)** validar con un contacto conocido independiente del mensaje, **(3)** avisar a IT, preservar el original e incluir al menos hora, canal, referencia y acciones realizadas. Registra el número de participantes, cuántos logran 3/3 y el error más frecuente. Si hay un error, vuelven a resolver una variante en el refuerzo de la semana 4.

### 3.2. Vinculación con el programa

- **Objetivo y acción:** O-01 y A-01.
- **Destinatarios:** Operaciones y Atención al Cliente.
- **Canal:** reunión de equipo y ficha disponible en el espacio corporativo propuesto.
- **Uso:** 3 minutos de lectura, 5 para resolver el caso, 4 para corregir y 3 para practicar el aviso. El facilitador guarda el recuento agregado de las decisiones evaluadas.
- **Ubicación:** apartado 3.1 de este documento.
