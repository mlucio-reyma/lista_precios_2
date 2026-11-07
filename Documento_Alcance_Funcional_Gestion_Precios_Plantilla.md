# RY-01INN01-FT01 Documento de Alcance Funcional

**Documento de Alcance Funcional**

**GRUPO REYES**

**Innovación y Negocios**

# Información General

|     |     |
|:----|:----|
| **Nombre del Proyecto** | Estandarización y Optimización de la Gestión de Precios |
| Número de Solicitud de Servicio | 16965 |
| Tipo de Servicio | Mejora Evolutiva |
| Prioridad | - [x] Urgente (Alta)   <br> - [ ] Medio  <br> - [ ] Bajo |
| Área de I&N Responsable de Implementación | Célula Reyma Comercial |
| Responsable del Requerimiento | Por definir |
| Fecha de Elaboración | 01/01/2026 (por definir) |
| Product Owner | Consultor |
| Área de Negocio | Ventas |
| Versión | 0.2 |
| Estado | - [x] Borrador  <br> - [ ] En validación  <br> - [ ] Aprobado  <br> - [ ] En Desarrollo |

# Resumen Ejecutivo (opcional para Configuración Operativa)

## 2.1 Objetivo del Proyecto

Sistematizar en el ERP de la empresa (R1) el cálculo y la definición del precio de venta que hoy hace el departamento de Ventas para sus clientes especiales, de autoservicio y de exportación. El sistema permitirá configurar, calcular, validar y gestionar esos precios de forma estandarizada.

## 2.2 Antecedentes

Ventas calcula hoy estos precios en archivos de Excel. Ahí reúne todos los elementos que intervienen en el precio, según las condiciones comerciales de cada cliente o grupo de clientes. Una vez autorizado el precio, se envía a Auditoría de Ventas en una lista de precios. Auditoría la carga en el sistema para que se pueda usar en la operación comercial.

## 2.3 Beneficio de Negocio

* Necesidad actual: reducir la dependencia de Excel y de la captura manual en el cálculo de precios.
* Impacto esperado: reglas de cálculo estandarizadas y controladas dentro del sistema, con menos errores y retrabajos.
* Beneficio operativo/comercial: información más confiable y fácil de rastrear, y una gestión de precios más ágil.

## 2.4 Descripción General de la Solución

Primero se configuran los elementos comerciales que definen el precio: claves de producto, listas base y reglas de cálculo. Con esa configuración, el sistema calcula el precio de cada lista (especial, autoservicio o exportación).

Ventas genera y revisa los precios resultantes y los valida. Después los lleva por el flujo de aprobación: Dirección, Cliente y autorización final. Solo entonces se consideran vigentes para la operación comercial. Una vez autorizados, quedan disponibles en el sistema mediante listas de precios detalladas.

Estatus de una lista: nace como *Capturada* y avanza en este orden: *Pendiente Aprobar Dirección → Aprobada Dirección → Pendiente Aprobar Cliente → Aprobada Cliente → Autorizada*. *Autorizada* es el único estatus final. También existen los estatus *Cancelada* y *No Autorizada*, que pueden reactivarse a *Capturada*.

La lista se envía a Dirección y al Cliente por correo, fuera del sistema. Al recibir la respuesta, un Autorizador la registra en el sistema: aprobación, aprobación con cambios o no autorización.

Transiciones permitidas:

| De | A | Quién |
|:--|:--|:--|
| *Capturada* | *Pendiente Aprobar Dirección* | Gestor de Listas |
| *Pendiente Aprobar Dirección* | *Aprobada Dirección* | Autorizador |
| *Aprobada Dirección* | *Pendiente Aprobar Cliente* | Gestor de Listas |
| *Pendiente Aprobar Cliente* | *Aprobada Cliente* | Autorizador |
| *Aprobada Cliente* | *Autorizada* | Usuario con permiso especial de autorización final |
| *Pendiente Aprobar Dirección*, *Pendiente Aprobar Cliente* (aprobación con cambios) | *Capturada* | Autorizador |
| *Pendiente Aprobar Dirección*, *Pendiente Aprobar Cliente* | *No Autorizada* | Autorizador |
| *Aprobada Cliente* | *No Autorizada* | Usuario con permiso especial de autorización final |
| Cualquier estatus, excepto *Autorizada* | *Cancelada* | Gestor de Listas |
| *Cancelada*, *No Autorizada* | *Capturada* | Gestor de Listas |

Cuando una lista regresa a *Capturada*, ya sea por aprobación con cambios o por reactivación, el Gestor de Listas la corrige y el proceso reinicia desde Dirección; las aprobaciones anteriores dejan de ser válidas. Cada cambio de estatus queda registrado en una bitácora (RN-015).

Actualmente la administración de listas de precios se divide en 2 grandes grupos: las listas de precios generales (bases y dependientes) y las listas de precios personalizadas. Existen varios tipos de listas personalizadas, las cuales son:

| Listas de Precio R1 |
|:----|
| Lista de Precios Especial Cliente |
| Lista de Precios Especial Autoservicio |
| Lista de Precios Especial Exportación |

En las listas personalizadas existen 4 clasificaciones de claves de producto que pueden utilizarse:

| Clase de clave | Observación |
|:----|:----|
| Clave Comercial | Claves de producto de uso general, aplicables en listas generales y también en listas de exportación cuando corresponda. |
| Clave Especial Cliente | Clave de producto definida o personalizada para un cliente específico, que mantiene una o varias características físicas que difieren de un producto comercial. |
| Clave Autoservicio | Claves de producto ofertadas a clientes de autoservicio, identificadas por su presentación diferente a la de una clave comercial. |
| Clave Exportación | Claves de producto destinadas a ventas de tipo exportación. |

Relación de claves de producto y tipos de listas:

| Tipo de Lista | Tipo de Claves de Producto |
|:----|:----|
| Lista de Precios Especial Cliente | Clave Comercial, Clave Especial Cliente |
| Lista de Precios Especial Autoservicio | Clave Autoservicio |
| Lista de Precios Especial Exportación | Clave Exportación, Clave Especial Cliente |

# Alcance Funcional

## 3.1 Funcionalidades Incluidas

* Configuración y gestión de las claves de producto que forman la estructura para determinar precios, incluida la relación entre clave especial y clave comercial.
* Configuración y gestión de las listas de precios especiales, de autoservicio y de exportación, con sus listas base (A y B).
* Configuración y aplicación de las reglas de negocio para calcular automáticamente el precio de venta.
* Generación de precios preliminares para revisarlos antes de aplicarlos.
* Revisión y aprobación de los precios calculados por usuarios autorizados, antes de su uso comercial.
* Consulta y control de la configuración y de los cambios hechos a los elementos que determinan el precio.
* Pantalla *Lista de Precios Personalizada* para agregar y modificar cada lista.
* Pantalla *Monitor de Lista de Precios Personalizadas* para dar seguimiento al ciclo de vida de las listas.

## 3.2 Fuera de Alcance (Muy Importante para Control de Cambios)

* Incorporación de nuevos tipos de lista no contemplados en el alcance.
* Cualquier cambio al funcionamiento de las funcionalidades aprobadas.
* Toda integración ajena al sistema como fuente de información.
* Los procesos de alta de clave comercial y de alta de clave especial, que ya existen. El proyecto solo trabaja la relación entre ambas.

# Requerimientos / Ajustes Funcionales (base para backlog)

|     |     |     |     |
|:----|:----|:----|:----|
| **ID** | **Nombre del Requerimiento** | **Descripción Funcional** | **Tipo (Story/Feature)** |
| RF-01 | Configuración de claves de producto del cliente | Relación entre las claves especiales (cliente, autoservicio, exportación) y la clave comercial. Una clave comercial puede tener varias claves especiales, y la relación se comparte entre clientes. Las claves especiales sin clave comercial son válidas y su precio inicial se captura a mano. Las cargas desde Excel incorporan un campo nuevo para la clave comercial. | Product Backlog |
| RF-02 | Configuración de listas de precios | Captura de listas en la pantalla Lista de Precios Personalizada (identificador, estatus, nombre, vigencia, tipo de lista, lista de referencia, lista base (a nivel general o por clave), clientes, observaciones, detalle de claves y sucursal). La sucursal se asigna automáticamente con la del usuario que crea la lista. El tipo de lista limita las claves y las listas de referencia que se pueden usar. Permite crear nuevas versiones de una lista existente. | Product Backlog |
| RF-03 | Definición del precio de referencia | El precio inicial viene de la lista base (A o B) vigente, de una lista base histórica o de captura manual (claves especiales sin clave comercial). Puede definirse a nivel general (aplica a toda la lista) o a nivel clave, y ambas formas pueden aplicarse en una misma lista. La clasificación de lista base (A o B) permitida para cada clave comercial viene del catálogo de claves. | Product Backlog |
| RF-04 | Determinación de proporcionalidad | Cuando la presentación de la clave del cliente difiere de la comercial, el precio base se ajusta con una fórmula parametrizable (v1 / v2) * v3. Los valores los captura el usuario y el resultado se redondea a 2 decimales. | Product Backlog |
| RF-05 | Aplicación de descuentos y sobreprecios | Aplicación de descuentos y sobreprecios como importe, porcentaje o importe relacionado con el cubicaje. | Product Backlog |
| RF-06 | Cálculo automático del precio de venta | Cálculo automático del precio de venta con las reglas y condiciones configuradas. Muestra el precio de referencia y los ajustes usados. | Product Backlog |
| RF-07 | Cálculo de precios de exportación | Desglose del IVA y conversión a dólares con el tipo de cambio definido. Muestra el precio en pesos, el tipo de cambio y el precio en dólares. | Product Backlog |
| RF-08 | Generación de precios preliminares | Generación de la lista preliminar con estatus *Capturada* y avance por el flujo de estatus. La lista se ve en el cuadrante del Monitor que corresponde a su estatus. | Product Backlog |
| RF-09 | Consulta y revisión de precios calculados | Consulta del detalle del cálculo: cliente, producto, precio de referencia, condiciones aplicadas y precio resultante. | Product Backlog |
| RF-10 | Validación y aprobación de precios | Aprobación de la lista por el flujo Dirección, Cliente y autorización final, sin saltar pasos. Se registra quién aprobó y cuándo. Los Autorizadores registran la respuesta de Dirección y del Cliente (aprobación, aprobación con cambios o no autorización), y la autorización final requiere el permiso especial (RN-014). Los Gestores de Listas envían la lista a cada paso, la cancelan antes de *Autorizada* y reactivan las listas *Cancelada* o *No Autorizada*. Transiciones según la sección 2.4. | Product Backlog |
| RF-11 | Generación de lista de precios autorizada | Generación o actualización de la lista autorizada. Permite recapturar y foncfirmar la fecha de inicio de vigencia, distinta a la de aprobación, y registrar el fin de vigencia. | Product Backlog |
| RF-12 | Control de modificaciones | Registro de las modificaciones a la información que determina los precios: qué se cambió, quién y cuándo. Incluye la bitácora de cambios de estatus de las listas (RN-015). | Product Backlog |
| RF-13 | Validaciones del proceso | Validación de la información requerida antes del cálculo. Si falta algo, el sistema lo indica y no calcula. | Product Backlog |
| RF-14 | Control de acceso | Acciones y listas visibles según el grupo del usuario (Gestores de Listas o Autorizadores), su sucursal y sus permisos especiales, conforme a RN-012, RN-013 y RN-014. | Product Backlog |
| RF-15 | Historial de precios | Consulta de precios anteriores, sus vigencias y la información asociada. Un precio histórico puede usarse como referencia. | Product Backlog |

# Requerimientos No Funcionales (si aplica)

|     |     |     |     |
|:----|:----|:----|:----|
| **ID** | **Nombre del Requerimiento** | **Descripción Funcional** | **Tipo (Story/Feature)** |
| RNF-01 | Seguridad | El sistema deberá garantizar el acceso controlado a las funcionalidades de gestión de precios mediante perfiles y permisos. Protegerá la información, configuraciones, reglas y precios contra modificaciones o accesos no autorizados. | Product Backlog |
| RNF-02 | Desempeño | El sistema deberá ejecutar las consultas, cálculos y actualizaciones de precios de manera eficiente, con tiempos de respuesta adecuados y resultados consistentes con las reglas configuradas. | Product Backlog |
| RNF-03 | Disponibilidad | El sistema deberá mantener disponibles las funcionalidades e información de precios durante el horario operativo establecido. También contará con mecanismos para recuperar la información ante interrupciones. | Product Backlog |
| RNF-04 | Trazabilidad | El sistema deberá permitir identificar el cliente, producto, precio de referencia y su origen (lista base vigente, lista base histórica o captura manual). También las reglas y condiciones aplicadas, el resultado, las modificaciones y los usuarios responsables del cálculo, revisión y aprobación. | Product Backlog |

# Reglas de Negocio

|     |     |
|:----|:----|
| **ID** | **Regla de Negocio** |
| RN-001 | Cada clave especial (cliente, autoservicio o exportación) se relaciona con una sola clave comercial, que sirve de referencia para el precio. Una clave comercial puede tener varias claves especiales, incluso de un mismo cliente, y la relación se comparte entre clientes. Pueden existir claves especiales sin clave comercial: su precio inicial se captura a mano. |
| RN-002 | El cálculo parte de un precio inicial previamente definido. Este viene de la lista base (A o B) vigente o histórica de la clave comercial, o de captura manual en las claves especiales sin clave comercial. No existe precio calculado por cliente ni cadenas de referencia. |
| RN-003 | Si la presentación de la clave del cliente difiere de la comercial, el precio se ajusta de forma proporcional con la fórmula parametrizable (v1 / v2) * v3, con base en las piezas o kilos del catálogo de productos. El resultado se redondea a 2 decimales. |
| RN-004 | Al precio ya ajustado se le aplican los descuentos y sobreprecios establecidos, como importe, porcentaje o importe relacionado con el cubicaje. |
| RN-005 | El precio de venta resulta de aplicar la proporcionalidad, los descuentos y los sobreprecios que correspondan a cada clave y cliente. |
| RN-006 | En exportación, el precio considera el desglose del IVA y después se convierte a dólares con el tipo de cambio definido. |
| RN-007 | Los precios calculados los revisa Ventas y avanzan por el flujo de estatus (Dirección, Cliente y autorización) antes de ser autorizados. Los Autorizadores aprueban los pasos de Dirección y Cliente; la autorización final la realiza quien tenga el permiso especial (RN-014). |
| RN-008 | Una vez aprobados los precios, se genera la lista de precios con los precios autorizados. |
| RN-009 | El tipo de lista (Especial Cliente, Autoservicio o Exportación) limita las claves que se pueden agregar: cada tipo usa su clase de clave. También limita las listas de referencia, que deben ser del mismo tipo **[a validar]**. |
| RN-010 | Toda lista nace como *Capturada* y avanza en este orden: *Pendiente Aprobar Dirección*, *Aprobada Dirección*, *Pendiente Aprobar Cliente*, *Aprobada Cliente* y *Autorizada*, sin saltar pasos. Solo se permiten las transiciones de la sección 2.4. La lista solo puede modificarse en *Capturada*. *Autorizada* es el único estatus final: no puede pasar a *No Autorizada* ni a *Cancelada*, ni reactivarse; para cambiarla se crea una nueva versión (RF-02). Las listas *Autorizada*, *Cancelada* y *No Autorizada* salen de los cuadrantes del Monitor y se consultan en su pestaña. Al reactivarse, una lista *Cancelada* o *No Autorizada* regresa al cuadrante de *Capturada*. |
| RN-011 | En el catálogo de claves se define, para cada clave comercial, la clasificación de lista base (A o B) en la que puede utilizarse. La A es para material termoespumado y la B para el resto. Al configurar la lista de precios, la lista base se aplica a nivel general o a nivel clave (ver RF-03), dentro de la clasificación que el catálogo permite a cada clave. |
| RN-012 | El acceso a las listas personalizadas se controla con dos grupos. **Gestores de Listas**: Ejecutivos de Ventas (también llamados Ejecutivos de Cuenta); capturan y modifican listas, las envían a Dirección y al Cliente, las cancelan y reactivan las listas *Cancelada* o *No Autorizada*. **Autorizadores**: Gerentes de Ventas, Gerentes Comerciales y Enlaces de Ventas; registran a nombre de Dirección y del Cliente la aprobación, la aprobación con cambios o la no autorización. Cualquier Autorizador puede pasar una lista a *No Autorizada*. |
| RN-013 | Los Autorizadores ven todas las listas personalizadas. Los Gestores de Listas ven solo las listas de su sucursal. La sucursal de la lista es la del usuario que la crea. La regla aplica al Monitor, a la consulta de listas y al historial. |
| RN-014 | El paso de *Aprobada Cliente* a *Autorizada* requiere el permiso especial **Autorizar Lista de Precios Personalizada**, que se asigna a una o varias personas en específico, sin importar su grupo. Quien tiene el permiso también puede pasar la lista de *Aprobada Cliente* a *No Autorizada*. El permiso no amplía la visibilidad: cada usuario solo puede autorizar las listas que puede ver según RN-013. Un Autorizador con el permiso puede autorizar listas de cualquier sucursal; un Gestor de Listas con el permiso, solo las de su sucursal. No hay restricción de separación de funciones: una misma persona puede registrar varias aprobaciones de una lista y dar su autorización final. |
| RN-015 | Cada cambio de estatus de una lista se registra en una bitácora con fecha, usuario, estatus anterior, estatus nuevo y un comentario o motivo opcional. La bitácora conserva todos los ciclos de la lista, incluidas las reactivaciones. |

**Nota: - Estas reglas pueden trasladarse como Criterios de Aceptación en los product backlogs / historias de usuario en Azure DevOps.**

# Criterios de Aceptación

Responsable de validación de todos los requerimientos: Product Owner y Área de Negocio (en RF-13, RF-14 y RF-15 solo el Product Owner). Los criterios marcados **[a validar]** son propuestas pendientes de confirmar.

## RF-01 Configuración de claves de producto del cliente

Dado que: el usuario autorizado registra la relación entre una clave especial y una clave comercial. Cuando: guarda la relación. Entonces: el sistema la conserva, la muestra en consulta y la usa como referencia del precio. Si la relación ya existe, bloquea el registro y muestra la existente **[a validar]**. Si la clave especial no tiene clave comercial, el sistema exige la captura manual del precio inicial **[a validar]**.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-02 Configuración de listas de precios

Dado que: el usuario autorizado configura una lista en la pantalla Lista de Precios Personalizada. Cuando: elige el tipo de lista. Entonces: el sistema ofrece solo las claves y listas de referencia de ese tipo. Si cambia el tipo con claves ya agregadas, avisa y las limpia. Muestra el cliente de referencia y el listado de clientes de la lista. Al crearla, asigna la sucursal del usuario que la crea. La casilla de lista de referencia se activa solo cuando la lista es nueva versión de una existente. Si falta algún campo obligatorio, indica cuál **[a validar]**.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-03 Definición del precio de referencia

Dado que: la clave necesita un precio inicial. Cuando: el usuario configura el origen del precio. Entonces: puede definir el origen a nivel general o a nivel clave, eligiendo lista base A o B (vigente o histórica) dentro de la clasificación que el catálogo de claves permite a la clave comercial, o captura manual si no hay clave comercial. El sistema usa la fuente configurada y conserva el origen utilizado.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-04 Determinación de proporcionalidad

Dado que: la presentación de la clave del cliente difiere de la comercial y requiere fórmula. Cuando: se ejecuta el cálculo. Entonces: el sistema aplica (v1 / v2) * v3 y redondea a 2 decimales. Si la presentación es igual o no requiere fórmula, conserva el precio de referencia. Si falta un valor o v2 es cero, impide el cálculo y señala el valor **[a validar]**.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-05 Aplicación de descuentos y sobreprecios

Dado que: hay un descuento o sobreprecio definido como porcentaje, importe o importe relacionado con el cubicaje. Cuando: se ejecuta el cálculo. Entonces: el sistema lo calcula según el tipo de condición configurado.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-06 Cálculo automático del precio de venta

Dado que: están configurados el producto, el precio de referencia y las condiciones comerciales. Cuando: el usuario ejecuta el cálculo. Entonces: el sistema determina el precio de venta y permite identificar el precio de referencia y los ajustes usados.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-07 Cálculo de precios de exportación

Dado que: se calcula el precio de una operación de exportación. Cuando: el sistema determina el precio. Entonces: considera el desglose del IVA, convierte a dólares con el tipo de cambio definido y permite ver el precio en pesos, el tipo de cambio y el precio en dólares.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-08 Generación de precios preliminares

Dado que: hay productos, clientes y condiciones configuradas. Cuando: el usuario genera una propuesta de precios. Entonces: el sistema crea la lista preliminar con estatus *Capturada*, evita que se considere autorizada y la muestra en el cuadrante del Monitor que corresponde a su estatus **[a validar: que la lista preliminar sea la lista Capturada]**.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-09 Consulta y revisión de precios calculados

Dado que: existe una lista preliminar. Cuando: un usuario autorizado la consulta. Entonces: el sistema muestra cliente, producto, precio de referencia, condiciones aplicadas y precio calculado, con información suficiente para identificar el origen de cualquier inconsistencia.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-10 Validación y aprobación de precios

Dado que: una lista está en proceso de aprobación. Cuando: el Gestor de Listas la envía a cada paso, un Autorizador registra la aprobación de Dirección y del Cliente, y un usuario con el permiso especial da la autorización final. Entonces: el sistema avanza su estatus hasta *Autorizada*. Solo permite las transiciones de la sección 2.4 y no permite saltar pasos.

* Si un Autorizador registra una aprobación con cambios, la lista regresa a *Capturada* y el proceso reinicia desde Dirección.
* En *Pendiente Aprobar Dirección* o *Pendiente Aprobar Cliente*, cualquier Autorizador puede pasarla a *No Autorizada*. En *Aprobada Cliente*, solo quien tiene el permiso especial. En *Capturada*, *Aprobada Dirección* y *Autorizada* no se ofrece esa opción.
* Sin el permiso especial, el sistema no ofrece la autorización final, aunque el usuario sea Autorizador.
* El Gestor de Listas puede cancelar la lista en cualquier estatus excepto *Autorizada*, y reactivar a *Capturada* una lista *Cancelada* o *No Autorizada*.
* Cada cambio de estatus queda en la bitácora con fecha, usuario, estatus anterior, estatus nuevo y comentario opcional (RN-015).

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-11 Generación de lista de precios autorizada

Dado que: los precios fueron aprobados. Cuando: concluye la autorización. Entonces: el sistema genera o actualiza la lista de precios con los precios autorizados y vigentes. Permite capturar la fecha de inicio de vigencia, independiente de la fecha de aprobación. Un usuario con permisos puede registrar la fecha de fin de vigencia, y después de esa fecha los precios no se pueden usar.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-12 Control de modificaciones

Dado que: un usuario autorizado modifica información de la determinación de precios. Cuando: guarda el cambio. Entonces: el sistema lo registra y permite consultar qué se modificó, quién lo hizo y cuándo.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

## RF-13 Validaciones del proceso

Dado que: falta información obligatoria o no existe un precio de referencia o condición necesaria. Cuando: el usuario intenta ejecutar el cálculo. Entonces: el sistema lo impide y muestra qué se debe completar. Una clave especial sin clave comercial no bloquea el cálculo, pero sí se bloquea si le falta el precio inicial capturado a mano **[a validar]**.

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

## RF-14 Control de acceso

Dado que: el usuario tiene un perfil y permisos determinados. Cuando: entra al módulo de gestión de precios. Entonces: el sistema muestra solo las acciones autorizadas para su perfil e impide modificar o aprobar precios a quien no tiene permiso. Un Gestor de Listas no ve ni puede abrir listas de otra sucursal. Un usuario sin el permiso especial no puede dar la autorización final.

Matriz de permisos:

| Acción | Gestores de Listas | Autorizadores |
|:--|:--:|:--:|
| Ver listas | Solo su sucursal | Todas |
| Crear / modificar lista (solo en *Capturada*) | ✔ | ✖ **[a validar]** |
| Enviar a Dirección (*Capturada* → *Pendiente Aprobar Dirección*) | ✔ | ✖ |
| Enviar al Cliente (*Aprobada Dirección* → *Pendiente Aprobar Cliente*) | ✔ | ✖ |
| Registrar aprobación de Dirección y del Cliente | ✖ | ✔ |
| Registrar aprobación con cambios (→ *Capturada*) | ✖ | ✔ |
| Marcar *No Autorizada* en *Pendiente Aprobar Dirección* o *Pendiente Aprobar Cliente* | ✖ | ✔ |
| Autorización final o *No Autorizada* desde *Aprobada Cliente* | Solo con permiso especial (su sucursal) | Solo con permiso especial |
| Cancelar (excepto *Autorizada*) | ✔ | ✖ **[a validar]** |
| Reactivar (*Cancelada* o *No Autorizada* → *Capturada*) | ✔ | ✖ |

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

## RF-15 Historial de precios

Dado que: existen precios de periodos anteriores. Cuando: un usuario autorizado consulta el historial de un producto o cliente. Entonces: el sistema muestra los precios determinados y su vigencia. Si se elige un precio histórico como referencia, el cálculo usa el precio de ese periodo. Las listas con vigencia terminada se conservan, con su periodo y fecha de fin, y no se pueden usar para nuevas operaciones.

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

# Supuestos y consideraciones

* Dependencias de negocio/proceso:
  * Ventas proporciona y valida las condiciones comerciales, reglas de cálculo, productos y relaciones entre claves.
  * Ventas revisa los precios calculados; los aprueban los Autorizadores y los autoriza quien tenga el permiso especial (RN-014).
  * Cada sucursal debe tener al menos una persona con el permiso de autorización final que pueda ver sus listas. Si no la hay, sus listas se quedan detenidas en *Aprobada Cliente*.
  * El área responsable define las fechas de inicio y fin de vigencia de las listas.
  * Las listas con vigencia terminada se conservan como historial y no se eliminan.
* Información de entrada requerida:
  * Clientes y listas de precios correspondientes.
  * Claves de producto del cliente y claves comerciales de referencia.
  * Presentaciones de producto, y piezas o kilos para la proporcionalidad.
  * Precios de referencia y su origen.
  * Descuentos, sobreprecios y demás condiciones comerciales.
  * Información para exportación, incluido el tipo de cambio.
  * Fechas de inicio y fin de vigencia de las listas.
* Dependencias técnicas:
  * Información maestra de clientes, productos y listas de precios disponible y consistente en R1.
  * Estructura disponible para configurar las reglas y condiciones del cálculo.
  * R1 debe conservar el historial de precios, vigencias y trazabilidad.
  * Mecanismo disponible para obtener el tipo de cambio de exportación.
* Integraciones involucradas:
  * Gestión de Ventas – Pedido de Venta, para aplicar el precio autorizado y vigente según cliente y producto.
* Servicios/APIs impactadas:
* Restricciones tecnológicas:

Para las mejoras evolutivas, indicar además los

* Sistemas y procesos impactados: R1, en el proceso de determinación y gestión de precios que hoy se hace en Excel.
* Grupos de usuarios afectados: Gestores de Listas (Ejecutivos de Ventas: captura, modificación y cancelación de listas) y Autorizadores (Gerentes de Ventas, Gerentes Comerciales y Enlaces de Ventas: revisión y aprobación de listas), además de los usuarios con el permiso especial de autorización final.
* Riesgos operativos asociados:
  * Información o condiciones comerciales incorrectas o incompletas que den un cálculo erróneo.
  * Fechas de vigencia mal definidas, que causen precios aplicados fuera del periodo autorizado.
  * Diferencias entre la información de Excel y la configurada en R1 durante la implementación.
  * Cambios en las condiciones comerciales que no estén contemplados en las reglas configuradas.
* otros efectos relevantes.

# Flujo Funcional / Proceso (si aplica)

[Insertar diagramas, imágenes o links de los flujos elaborados]

# Diseño Funcional (Wireframes / Mockups si aplica)

|     |     |     |
|:----|:----|:----|
| **Pantalla** | **Descripción** | **Referencia** |
| Pantalla 1. Lista de Precios Personalizada | Permite configurar nombre, tipo de lista, vigencia, lista base del precio, lista detallada a la que se aplicará y claves de producto del cliente. Muestra la relación entre la clave del cliente y la clave comercial equivalente, el precio base referenciado y el precio determinado al cliente según las operaciones del cálculo. | [Imagen/Link] |
| Pantalla 2. Agregar operaciones | Permite elegir cómo se aplican los descuentos y sobreprecios a las claves del cliente. Muestra el orden de aplicación capturado por el usuario autorizado. | [Imagen/Link] |
| Pantalla 3. Operaciones | Muestra los cálculos hechos por el sistema con los parámetros configurados en la pantalla anterior. | [Imagen/Link] |
| Pantalla 4. Monitor de Lista de Precios Personalizadas | Pantalla principal de seguimiento del ciclo de vida de las listas, dividida en 5 cuadrantes por estatus: *Capturada*, *Pendiente Aprobar Dirección*, *Aprobada Dirección*, *Pendiente Aprobar Cliente* y *Aprobada Cliente*. Los cuadrantes muestran solo las listas que el usuario puede ver según su grupo y sucursal (RN-013). Desde ahí se llama a la pantalla Lista de Precios Personalizada para agregar o modificar listas, y se ejecutan los cambios de estatus permitidos (sección 2.4). Incluirá una pestaña para las listas *Autorizada*, *Cancelada* y *No Autorizada*, desde la que se reactivan las canceladas y no autorizadas (sin wireframe todavía). | [Imagen pendiente] |

# Impacto Organizacional y Requerimientos de Capacitación

[Identificación de las áreas de negocio, roles de usuario y componentes funcionales que serán impactados por la implementación del proyecto, así como los requerimientos de capacitación, generación de material necesarios para asegurar la adopción del sistema y cantidad de capital humano a desarrollar]

## 11.1 Áreas y Roles impactados

| **Área** | **Rol** | **Tipo de Usuario** | **Capacitación Requerida** |
|:-----|:----|:----------------|:-----------------------|
| Ventas | Gestores de Listas (Ejecutivos de Ventas) | Operativo | Sí |
| Ventas | Autorizadores (Gerentes de Ventas, Gerentes Comerciales y Enlaces de Ventas) | Aprobador | Sí |
| Ventas | Usuarios con permiso especial de autorización final | Autorizador final | Sí |

## 11.2. Componentes funcionales que requieren material de capacitación

| **Módulo** | **Proceso** | **Pantalla / Catálogo** | **Tipo de Cambio**<br>\*\*(Nuevo / Modificación)\*\* | **Cantidad de capital Humano** |
|:-------|:--------|:--------------------|:------------------------------------------|----------------------------|
| Gestión de Precios | Solicitud de Cambio | Solicitud de Cambio de Precio | Nuevo                                     | 5                          |
| Gestión de Precios | Aprobación | Bandeja de Aprobaciones | Nuevo                                     | 4                          |
| Configuración | Catálogo | Categorías Comerciales | Modificación                              | 3                          |
| Configuración | Catálogo | Grupos de Precio    | Nuevo                                     | 2                          |
| Reportes | Consulta | Histórico de Cambios | Nuevo                                     | 1                          |

# Riesgos e Impactos Identificados

|     |     |     |
|:----|:----|:----|
| Tipo | Descripción | Mitigación |
| Operativo | Las respuestas de Dirección y del Cliente se registran sin evidencia adjunta y sin separación de funciones: una misma persona puede registrar todas las aprobaciones de una lista y dar su autorización final. | Decisión aceptada por el negocio. La bitácora de estatus (RN-015) permite rastrear quién registró cada paso; se recomienda usar el comentario para indicar el origen de la respuesta. |
| Técnico |     |     |
| Negocio |     |     |

**(matriz de riesgo)**

# Aprobaciones

**Mediante la firma del presente documento, el usuario solicitante manifiesta haber revisado y validado el contenido del Documento de Requerimientos del Sistema, confirmando que los requerimientos, alcances, funcionalidades y consideraciones aquí descritas reflejan de manera correcta sus necesidades y expectativas. Asimismo, acepta que este documento servirá como base para las actividades de análisis, diseño, desarrollo e implementación de la solución tecnológica correspondiente.**

|     |     |     |     |
|:----|:----|:----|:----|
| **Área** | **Nombre** | **Firma / VoBo** | **Fecha** |
| Usuario |     |     |     |
| Consultor (Product Owner) |     |     |     |
| Coordinador de Desarrollo |     |     |     |
| Aseguramiento de Calidad de Software (opcional) |     |     |     |

# Control de Cambios

|     |     |     |     |
|:----|:----|:----|:----|
| **Versión** | **Fecha** | **Descripción del Cambio** | **Autor** |
| v1.0 | [Fecha] | Creación del documento |     |
| v1.1 | [Fecha] | Ajustes por validación |     |

# ANEXOS (Opcional)

* Minutas de sesión
* Evidencia de validación
* Correos de aprobación
* Documentos complementarios
