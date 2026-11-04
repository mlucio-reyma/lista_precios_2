![](media/media/image1.png)

**Documento de Alcance Funcional**

**GRUPO REYES**

**Dirección de Innovación y Negocios**

**Consultoría**

## Información General

| Campo | Valor |
|---|---|
| Fecha de Elaboración | 01/01/2026 (por definir, ver sección 9, G-2) |
| Fecha de actualización | 26/10/2026 |
| No. de solicitud de servicio | 16965 |
| Nombre del Proyecto | Estandarización y Optimización de la Gestión de Precios |
| Tipo de Servicio | ☐ Sistema Nuevo · ☒ Mejora Evolutiva · ☐ Configuración Operativa |
| Prioridad | ☒ Alta · ☐ Media · ☐ Baja |
| Área de I&N Responsable de Implementación | Célula Reyma Comercial |
| Responsable del Requerimiento | Por definir (ver sección 9, G-1) |
| Producto Owner | Consultor |
| Área de Negocio | Ventas |
| Versión | 0.2 |
| Estado | ☒ Borrador · ☐ En Validación · ☐ Aprobado · ☐ En Desarrollo |

> **Nota de esta versión.** Esta versión 0.2 deriva de la versión 0.1 e incorpora el contexto y las respuestas de la Product Owner entre el 22 y el 26/10/2026. Lo que la PO ya confirmó se redacta como definición firme. Lo que es propuesta pendiente de validación se marca con **[a validar]**. Los criterios de aceptación nuevos que provienen de una propuesta y no de una respuesta de la PO se marcan **(nuevo, a validar)**. Las preguntas aún abiertas están en la sección 9.

# Contexto (explicación del producto)

Actualmente la administrcón de listas deprecios se divide en 2 grandes grupos, las listas de precio generales (bases y dependientes) y las listas de precios personalizadas. Existen varios tipos de listas personalizadas las cuales son:

| Lista de Precios Especial Cliente |
| Lista de Precios Especial Autoservicio |
| Lista de Precios Especial Exportación |

En las listas personalizadas existen 4 clasificaciones de claves de producto que pueden utilizarse las cuales son:

| Clase de clave | Observación | 
|---|---|
| Clave Comercial | Claves de producto de uso general, aplicables en listas generales y también en listas de exportación cuando corresponda |
| Clave Especial Cliente | Clave de producto definidas o perzonalizdas para un cliente especifico, mantiendo una o varias caracteriscas fisicas que difieren de un producto comercial |
| Clave Autoservicio  | Claves de productos ofertadas a clientes de autoservicio identificadas por su presentacion difeente a una clave comercial |
| Clave Exportación  | Claves de producto destinada para ventas de tipo exportacion |

Relacion de Claves de Prodcutos y Tipos de listas

| Tipo de Lista | Tipo de Claves de Producto |
| --- | --- |
| Lista de Precios Especial Cliente | - |
| Lista de Precios Especial Autoservicio | - |
| Lista de Precios Especial Exportación | - |


## C.1 Conceptos base



**Clasificación de claves de producto.** El proyecto trabaja con 4 clases de clave. Cada tipo de lista utiliza su tipo de clave correspondiente:

|

**Relación entre clave especial y clave comercial.** Las reglas aplican igual a las tres clases de clave especial (Cliente, Autoservicio y Exportación):

- La mayoría de las veces, una clave especial tiene relación directa con **una sola** clave comercial.
- Sin embargo pueden existir claves especiales **sin clave comercial relacionada**, en las tres clases. Su precio inicial se captura a mano.
- Varias claves especiales de la misma clase pueden relacionarse con una misma clave comercial, incluso las de un mismo cliente (relación muchas a una).
- La relación es **compartida** entre clientes: la puede usar más de un cliente o grupo de clientes.
- Los procesos de alta de clave comercial y de clave especial ya existen. El proyecto solo trabaja la **relación** entre ambas.
- Para el caso de las cargas masivas de claves desde Excel es necesario incorporan un campo nuevo para la clave comercial. (Desarrollar como feature)

## C.2 Glosario

| Término | Significado en este documento |
|---|---|
| **Claves Especiales** (también *Claves de Clientes*) | El grupo formado por las 3 clases: Clave Especial Cliente, Clave Autoservicio y Clave Exportación |
| **Clave Especial Cliente** | Una de las 3 clases del grupo, usada por la Lista Especial Cliente. No tiene relacion con los grupos de clientes|
| **Clave Comercial** | Clave del catálogo comercial a la que se relacionan las Claves Especiales |
| **Clave especial sin clave comercial** | Clave especial de cualquiera de las 3 clases sin relación con una clave comercial. Su precio inicial se captura a mano |
| **Lista Base A / Lista Base B** | Listas de las que se obtiene el precio base de una clave comercial. Cada clave comercial pertenece a una según las características del producto |
| **Lista detallada de referencia** | Lista de precios detallada de R1 (producto por producto) de la que parte la cotización y que se actualiza al autorizar la cotizacion de precios |

## C.3 Listas base A y B

Hoy el precio base de una Clave Comercial se obtiene de 2 listas base (A y B). Las claves se reparten entre ambas según las características del producto:

| Lista base | Productos |
|---|---|
| A | Material termoespumado |
| B | El resto de los productos (no termoespumados) |

La lista (A o B) a la que pertenece cada clave comercial se define en el **catálogo de claves**. No se asigna al configurar la lista de precios. Las listas base A y B aplican igual a los tres tipos de lista.

## C.4 Pantalla principal de captura: Cotizador de Lista de Precios Personalizada

La idea central del proyecto es generar varias pantallas de trabajo. Una de ellas, llamada temporalmente **"Cotizador de Lista de Precios Personalizada"** (pantalla 1 de los wireframes), es la pantalla a la que se refiere RF-02. Reúne esta información, común a los tres tipos de lista:

| Dato | Descripción |
|---|---|
| Identificador único | Identifica la lista (ejemplo: LC-0045) |
| Estatus | Capturada, Pendiente Aprobar Dirección, Pendiente Aprobar Cliente, Pendiente Autorizar, Autorizada, Cancelada, No Autorizada (ver C.5) |
| Nombre | Nombre de la lista |
| Fechas de inicio y fin de vigencia | Periodo de la lista |
| Tipo de lista de precios | Especial Cliente, Autoservicio o Exportación |
| Lista de precios detallada de referencia | Lista de la que parte la cotización. Se actualiza al autorizar |
| Lista base A y Lista base B | Listas de origen del precio base (ver C.3) |
| Clientes | Un cliente como referencia y el listado de todos los clientes a los que aplica la lista (botón *Ver clientes*) |
| Observaciones | Texto libre |
| Detalle de productos de la lista | Orden, Clave, Descripción, Clave comercial relacionada, Precio base y Precio final |

**El tipo de lista como filtro.** La clasificación por tipo de lista acota las claves de producto y las listas de referencia que se pueden usar al crear una lista nueva. No se necesita una relación entre tipo de lista y listas base A y B. Si el usuario cambia el tipo de lista cuando ya agregó claves, el sistema muestra una advertencia y limpia las claves para una nueva captura. Una lista solo toma como referencia otra lista del mismo tipo **[a validar]**.

**Nueva versión de una lista.** Cuando la lista es la nueva versión de una lista ya existente, se activa la casilla de la lista detallada de referencia. En una lista personalizada nueva, creada desde cero, la casilla no se activa.

**Claves sin clave comercial en el Cotizador.** Las claves sin clave comercial relacionada se muestran sin clave comercial equivalente y con el precio base editable (captura manual). El wireframe las identifica con el marcador y el contador *Precio base manual*.

## C.5 Estatus de las listas y flujo

Por ahora, las listas de precios personalizadas usan estos estatus:

| Estatus |
|---|
| Capturada |
| Pendiente Aprobar Dirección |
| Pendiente Aprobar Cliente |
| Pendiente Autorizar |
| Autorizada |
| Cancelada |
| No Autorizada |

Todas las listas nacen como *Capturada* y avanzan en este orden:

*Capturada → Pendiente Aprobar Dirección → Pendiente Aprobar Cliente → Pendiente Autorizar → Autorizada*

Al llegar a *Autorizada*, la lista sale de los cuadrantes del Monitor. Las listas *Autorizada*, *Cancelada* y *No Autorizada* se visualizan en una **pestaña nueva dentro del Monitor** (aún sin imagen de ejemplo).

El estatus *En negociación* que aparece en el wireframe del Cotizador equivale a *Pendiente Aprobar Cliente* y era solo un ejemplo de estatus. No es un estatus aparte.

Las salidas a *Cancelada* y *No Autorizada* (desde qué estatus, quién las decide y qué pasa con una lista rechazada) están pendientes de definir (sección 9).

## C.6 Pantalla principal de seguimiento: Monitor de Lista de Precios Personalizadas

Es la pantalla principal de trabajo. Mantiene a la vista el **ciclo de vida** de las listas de precios personalizadas, dividido en cuadrantes. Las columnas del wireframe son solo referencia de información y no son necesariamente las que se usarán.

| Cuadrante | Estatus que muestra |
|---|---|
| Capturadas | Capturada |
| Pendiente Autorizar Dirección | Pendiente Aprobar Dirección |
| Pendiente Autorizar Cliente | Pendiente Aprobar Cliente |
| Pendiente de Autorizar | Pendiente Autorizar |

Operaciones previstas desde el Monitor:

- Llamar al *Cotizador de Lista de Precios Personalizada* para **agregar** o **modificar** listas.
- **Autorizar** o **cancelar** listas personalizadas.
- La PO describirá más operaciones disponibles desde esta pantalla. Las acciones visibles en el wireframe son Agregar, Guardar, Cancelar, Actualizar información, Mostrar paneles, Mostrar pedidos sucursales y Quitar filtros personalizados; cuáles aplican queda por definir.

## C.7 Mapa mental (versión preliminar)

La PO compartió un mapa mental como **primer acercamiento** al proyecto, que se irá detallando y ajustando. No es una regla definitiva. Alrededor de *Listas Personalizadas* muestra:

| Pieza | Contenido en el mapa |
|---|---|
| Tipos de lista | Especial Cliente, Autoservicio y Exportación, cada una ligada a sus claves (en el mapa falta el nodo *Clave Autoservicio*) |
| Precio por clave | El precio inicial se extrae de una lista base (A o B), vigente o histórica |
| Clave especial | Con clave comercial relacionada o sin clave relacionada |
| Presentación del producto | Proporción del precio |
| Sobreprecios | Por criterio, importe fijo o porcentaje sobre el precio inicial |
| Descuentos | Por criterio o importe fijo |
| Criterios | Sin detalle todavía |

# 1. Resumen Ejecutivo

## 1.1 Objetivo del Proyecto

Sistematizar y automatizar el proceso de cálculo y determinación del precio de venta que realiza el departamento de Ventas para sus clientes especiales, autoservicio y exportación, mediante la implementación de una estructura funcional en el sistema que permita configurar, calcular, validar y gestionar los precios de manera estandarizada.

## 1.2 Antecedentes

Actualmente, el departamento de Ventas realiza el cálculo y determinación de los precios de venta para clientes especiales, autoservicio y exportación mediante archivos de Excel. En estos archivos se concentran y procesan diferentes elementos que intervienen en la determinación del precio, de acuerdo con las condiciones comerciales establecidas para cada cliente o grupo de clientes.

Una vez autorizado el precio lo envían al área de Auditoria de Ventas mediante una lista de precios para que lo cargue en el sistema para la operación comercial.

## 1.3 Beneficio de Negocio

La sistematización y automatización del cálculo de precios de venta para clientes especiales, autoservicio y exportación permitirá estandarizar y controlar las reglas de determinación de precios dentro del sistema, reduciendo la dependencia de archivos de Excel y la intervención manual. Esto contribuirá a disminuir errores y retrabajos, mejorar la trazabilidad y confiabilidad de la información, y agilizar la gestión de precios.

## 1.4 Descripción General de la Solución

El proceso iniciará con la configuración de los elementos comerciales que intervienen en la determinación del precio, considerando claves de productos, listas base y las condiciones o reglas de cálculo aplicables. A partir de esta configuración, el sistema deberá utilizar las reglas definidas para determinar los precios correspondientes a cada lista (especial, autoservicio y exportación).

Como parte del flujo, Ventas podrá generar y revisar los precios resultantes, realizar las validaciones correspondientes y, de acuerdo con el proceso establecido, gestionar su aprobación antes de que sean considerados como precios vigentes para la operación comercial. Una vez autorizados, los precios estarán disponibles en el sistema para su aplicación mediantes listas de precios detalladas.

De forma general, el flujo esperado será:![](media/media/image2.png)

# 2. Alcance Funcional

## 2.1 Solución 

## 2.1.1 Funcionalidades Incluidas

- Permitir la configuración y gestión de claves de producto que conforman la estructura para la determinación de precios.

- Permitir la configuración y gestión de las listas de precios especiales, autoservicio y exportación, considerando las listas base correspondientes.

- Permitir la configuración y aplicación de las reglas de negocio necesarias para calcular automáticamente los precios de venta a partir de las condiciones definidas.

- Generar los precios preliminares derivados de los cambios o condiciones configuradas para su revisión antes de su aplicación.

- Revisar y aprobar de los precios calculados por parte de los usuarios autorizados antes de que sean utilizados en la operación comercial.

- Consultar y mantener el control sobre la configuración y los cambios realizados en los elementos que intervienen en la determinación de precios.

## 2.1.2 Fuera de Alcance (Muy Importante para Control de Cambios)

- La incorporación de nuevos tipos de listas no contemplados en el alcance.

- Todo cambio al funcionamiento o comportamiento de las funcionalidades aprobadas

- Toda integración ajena al sistema como fuente de información

- Los procesos de alta de clave comercial y de alta de clave especial, que ya existen. El proyecto solo trabaja la relación entre ambas.

## 2.2 Requerimientos / Ajustes Funcionales (base para backlog)

Cada requerimiento se describe en una ficha con su descripción funcional, las reglas de negocio vinculadas, sus criterios de aceptación, el responsable de validación y las dudas abiertas. La sección 3 remite a estas fichas. El detalle completo de las dudas está en la sección 9.

| ID | Nombre del Requerimiento | Resumen |
|---|---|---|
| RF-01 | Configuración de claves de producto del cliente | Relación entre claves especiales (cliente, autoservicio, exportación) y la clave comercial; precio inicial manual para claves sin relación. |
| RF-02 | Configuración de listas de precios | Configuración de listas en el Cotizador; el tipo de lista acota claves y listas de referencia; versionado de listas. |
| RF-03 | Definición del precio de referencia | Origen del precio inicial: lista base vigente, lista base histórica o captura manual. |
| RF-04 | Determinación de proporcionalidad | Ajuste proporcional mediante fórmula parametrizable (v1 / v2) * v3, redondeada a 2 decimales. |
| RF-05 | Aplicación de descuentos y sobreprecios | Descuentos y sobreprecios por importe, porcentaje o cubicaje. |
| RF-06 | Cálculo automático del precio de venta | Cálculo automático del precio de venta con las reglas configuradas. |
| RF-07 | Cálculo de precios de exportación | Precio de exportación: desglose de IVA y conversión a dólares con el tipo de cambio. |
| RF-08 | Generación de precios preliminares | Generación de la lista preliminar (estatus Capturada) y flujo de estatus. |
| RF-09 | Consulta y revisión de precios calculados | Consulta y revisión del detalle del cálculo de la lista. |
| RF-10 | Validación y aprobación de precios | Aprobación de la lista por el flujo Dirección, Cliente y autorización final. |
| RF-11 | Generación de lista de precios autorizada | Generación o actualización de la lista autorizada y gestión de su vigencia. |
| RF-12 | Control de modificaciones | Registro de modificaciones a la información que determina los precios. |
| RF-13 | Validaciones del proceso | Validación de la información requerida antes de ejecutar el cálculo. |
| RF-14 | Control de acceso | Acciones permitidas según el perfil y los permisos del usuario. |
| RF-15 | Historial de precios | Consulta del historial de precios, vigencias e información asociada. |

### RF-01 Configuración de claves de producto del cliente

**Descripción funcional**

Dado que cada cliente puede manejar claves especiales (de cliente, autoservicio o exportación) relacionadas con una clave de producto comercial, y que las altas de ambas claves ya existen en el sistema,  
cuando el usuario autorizado registre o modifique la relación entre una clave especial y una clave comercial,  
entonces el sistema deberá conservar dicha relación y utilizar la clave comercial como referencia para la determinación del precio. Cada clave especial se relaciona con una sola clave comercial, y una clave comercial puede tener varias claves especiales, incluso de un mismo cliente. La relación se comparte entre clientes. Las claves especiales sin clave comercial relacionada son válidas: su precio inicial se captura a mano. Las cargas actuales desde Excel incorporarán un campo nuevo para la clave comercial.

**Reglas de negocio vinculadas:** RN-001

**Criterios de aceptación**

CA-01.1 Dado que el cliente cuenta con claves de producto que requieren una referencia comercial, cuando el usuario autorizado registre la relación entre la clave del cliente y la clave comercial, entonces el sistema deberá guardar dicha relación y mostrarla en la consulta correspondiente.

CA-01.2 Dado que una clave especial (de cliente, autoservicio o exportación) tiene una clave comercial asociada,  
cuando se ejecute el cálculo del precio, entonces el sistema deberá utilizar la clave comercial configurada como referencia para determinar el precio.

CA-01.3 (nuevo, a validar) Dado que la relación entre la clave especial y la clave comercial ya está registrada, cuando el usuario intente registrarla de nuevo, entonces el sistema deberá bloquear la operación y mostrar la relación existente.

CA-01.4 (nuevo, a validar) Dado que una clave especial no tiene clave comercial relacionada, cuando se calcule la lista de precios, entonces el sistema deberá exigir la captura manual del precio inicial y utilizarlo como punto de partida del cálculo. **[a validar: si después continúa con proporcionalidad y operaciones o si ese precio ya es el final]**

CA-01.5 (nuevo, a validar) Dado que las cargas desde Excel incorporan un campo nuevo para la clave comercial, cuando el usuario cargue un archivo, entonces el sistema deberá relacionar cada clave especial con la clave comercial indicada en ese campo. **[a validar: tratamiento de filas con el campo vacío o con una clave comercial inexistente]**

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-01.1 (presentaciones de varias claves especiales de un mismo cliente); P-01.4 (qué sigue tras capturar el precio a mano y cómo se identifican esas claves); P-01.5 (flecha de Exportación hacia Clave Especial Cliente); P-01.6 (quién modifica la relación compartida).

### RF-02 Configuración de listas de precios

**Descripción funcional**

Dado que Ventas requiere administrar diferentes tipos de listas de precios para sus clientes,  
cuando el usuario autorizado configure en el *Cotizador de Lista de Precios Personalizada* una lista especial, de autoservicio o de exportación,  
entonces el sistema deberá permitir capturar los datos de la lista (identificador único, estatus, nombre, vigencia, tipo de lista, lista detallada de referencia, listas base A y B, clientes, observaciones y detalle de claves) y acotar, según el tipo de lista, las claves de producto y las listas de referencia que pueden utilizarse. Los tres tipos de lista usan los mismos campos.

**Reglas de negocio vinculadas:** RN-009, RN-011

**Criterios de aceptación**

CA-02.1 Dado que el usuario autorizado requiere configurar una lista de precios en el Cotizador,  
cuando seleccione el tipo de lista correspondiente a especial, autoservicio o exportación,  
entonces el sistema deberá permitir configurar los clientes, productos y condiciones comerciales correspondientes, ofreciendo únicamente las claves de producto de la clase que corresponde a ese tipo y las listas de referencia permitidas para ese tipo **[a validar: que las listas de referencia sean solo del mismo tipo]**.

CA-02.2 Dado que una lista de precios se encuentra configurada, cuando el usuario consulte su información, entonces el sistema deberá mostrar las condiciones y referencias asociadas a dicha lista.

CA-02.3 Dado que una lista aplica a más de un cliente, cuando el usuario consulte los clientes de la lista, entonces el sistema deberá mostrar el cliente de referencia y el listado de todos los clientes a los que aplica.

CA-02.4 Dado que el usuario ya agregó claves a la lista, cuando cambie el tipo de lista, entonces el sistema deberá mostrar una advertencia y limpiar las claves para una nueva captura.

CA-02.5 Dado que la lista se crea desde cero, cuando el usuario capture la lista, entonces la casilla de la lista detallada de referencia no deberá activarse. Dado que la lista es la nueva versión de una lista ya existente, entonces la casilla deberá activarse.

CA-02.6 (nuevo, a validar) Dado que se crea una lista sin fechas de vigencia, cuando el usuario intente guardarla, entonces el sistema deberá indicar el campo faltante. **[a validar: qué campos son obligatorios]**

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-02.1 (campos obligatorios); P-02.3 (cliente de referencia y listado); P-02.5 (entrega inicial de la lista Especial); P-02.8 (listas de referencia del mismo tipo, por confirmar); P-02.10 (identificación de una nueva versión); P-02.11 (qué se copia a la nueva versión); comportamiento si una clave comercial no tiene lista base en el catálogo.

### RF-03 Definición del precio de referencia

**Descripción funcional**

Dado que el precio inicial de una clave puede determinarse a partir de diferentes fuentes,  
cuando el usuario configure el origen del precio para realizar un cálculo,  
entonces el sistema deberá permitir seleccionar si el precio proviene de la lista base (A o B) vigente, de una lista base histórica (no vigente, pasada) o de una captura manual (en claves especiales sin clave comercial), y conservar dicha referencia. No existe precio calculado por cliente ni cadenas de referencia. El origen puede definirse a nivel general o a nivel detalle (por clave).

**Reglas de negocio vinculadas:** RN-002, RN-011

**Criterios de aceptación**

CA-03.1 Dado que el precio de una clave de producto con clave comercial requiere un precio inicial, cuando el usuario configure el origen del precio, entonces el sistema deberá permitir seleccionar la lista base (A o B, según el catálogo de claves) vigente o una lista base histórica como fuente de referencia.

CA-03.2 Dado que una clave especial no tiene clave comercial relacionada, cuando el usuario defina su precio inicial, entonces el sistema deberá permitir la captura manual del precio.

CA-03.3 Dado que se ha definido un precio de referencia, cuando se ejecute el cálculo, entonces el sistema deberá utilizar el precio correspondiente a la fuente configurada y conservar el origen utilizado.

CA-03.4 (nuevo, a validar) Dado que el origen del precio puede definirse a nivel general o a nivel detalle, cuando el usuario configure la lista, entonces el sistema deberá permitir definir el origen para toda la lista o para una clave. **[a validar: qué prevalece si hay una definición general y otra por clave, y cómo se elige una lista histórica]**

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-03.6 (prevalencia entre origen general y por clave, y elección de la lista histórica).

### RF-04 Determinación de proporcionalidad

**Descripción funcional**

Dado que la presentación de una clave de producto del cliente puede ser diferente a la de su clave comercial de referencia,  
cuando el sistema realice el cálculo del precio de una clave que lo requiera,  
entonces deberá aplicar el ajuste proporcional mediante una fórmula de la forma (v1 / v2) \* v3, cuyos valores introduce el usuario, y redondear el resultado a 2 decimales. Si el precio se calcula por piezas o por kilos y cuántas piezas contiene la presentación se toman del catálogo de productos. No existe una fórmula fija.

**Reglas de negocio vinculadas:** RN-003

**Criterios de aceptación**

CA-04.1 Dado que la clave de producto del cliente tiene una presentación diferente a la clave comercial de referencia y que la clave requiere fórmula, cuando se ejecute el cálculo, entonces el sistema deberá determinar la proporcionalidad aplicando la fórmula (v1 / v2) \* v3 con los valores introducidos por el usuario, y redondear el resultado a 2 decimales. **[a validar: significado de v1, v2 y v3]**

CA-04.2 Dado que la clave del cliente y la clave comercial tienen la misma presentación o que la clave no requiere fórmula,  
cuando se ejecute el cálculo, entonces el sistema deberá conservar el precio de referencia sin aplicar un ajuste de proporcionalidad.

CA-04.3 (nuevo, a validar) Dado que falta un valor de la fórmula o que v2 es igual a cero, cuando se ejecute el cálculo, entonces el sistema deberá impedir el cálculo y señalar el valor que requiere atención.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-04.4 (redondeo en pasos intermedios); P-04.5 (significado de v1, v2 y v3); P-04.6 (forma de la fórmula y dónde se captura); P-04.7 (unidades distintas entre clave comercial y especial).

### RF-05 Aplicación de descuentos y sobreprecios

**Descripción funcional**

Dado que existen descuentos y sobreprecios definidos de acuerdo con las condiciones comerciales,  
cuando el sistema determine el precio de una clave de producto,  
entonces deberá aplicar los descuentos y sobreprecios correspondientes considerando el tipo de cálculo configurado, ya sea importe, porcentaje o importe relacionado con el cubicaje.

**Reglas de negocio vinculadas:** RN-004

**Criterios de aceptación**

CA-05.1 Dado que un descuento o sobreprecio está definido como porcentaje, importe o importe relacionado con el cubicaje, cuando se ejecute el cálculo, entonces el sistema deberá realizar el cálculo conforme al tipo de condición configurado.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-05.1 (operaciones disponibles); P-05.2 (fuentes Calculado, Guardado y Fijo); P-05.3 (cubicaje y costo de flete); P-05.4 (orden de aplicación); P-05.5 (porcentaje sobre precio acumulado o base); P-05.6 (categoría de producto); P-05.7 (qué es un criterio); P-05.8 (descuento en porcentaje).

### RF-06 Cálculo automático del precio de venta

**Descripción funcional**

Dado que se encuentran configurados el producto, precio de referencia y condiciones comerciales requeridas,  
cuando el usuario ejecute el cálculo de precios,  
entonces el sistema deberá determinar automáticamente el precio de venta aplicando las reglas y condiciones correspondientes.

**Reglas de negocio vinculadas:** RN-002, RN-003, RN-004, RN-005

**Criterios de aceptación**

CA-06.1 Dado que se encuentran configurados el producto, precio de referencia y condiciones comerciales requeridas, cuando el usuario ejecute el cálculo, entonces el sistema deberá determinar automáticamente el precio de venta aplicando las reglas configuradas.

CA-06.2 Dado que el cálculo ha sido ejecutado, cuando el sistema muestre el resultado,  
entonces deberá permitir identificar el precio de referencia y los ajustes utilizados para obtener el precio de venta.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-06.1 (orden de la cadena de cálculo); P-06.2 (redondeo); P-06.3 (cuándo se recalcula); P-06.4 (clave sin operaciones); P-06.5 (recálculo según el estatus).

### RF-07 Cálculo de precios de exportación

**Descripción funcional**

Dado que las operaciones de exportación requieren determinar el precio en dólares,  
cuando el sistema realice el cálculo del precio de exportación,  
entonces deberá considerar el desglose del IVA y convertir el importe a dólares utilizando el tipo de cambio definido para la determinación del precio.

**Reglas de negocio vinculadas:** RN-006

**Criterios de aceptación**

CA-07.1 Dado que se está calculando el precio de una operación de exportación, cuando el sistema determine el precio, entonces deberá considerar el desglose del IVA conforme a la condición configurada.

CA-07.2 Dado que el precio de exportación debe expresarse en dólares, cuando se ejecute la conversión, entonces el sistema deberá utilizar el tipo de cambio definido para la determinación del precio.

CA-07.3 Dado que el cálculo de exportación ha sido realizado, cuando el usuario consulte el resultado, entonces deberá poder identificar el precio en pesos, el tipo de cambio utilizado y el precio resultante en dólares.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-07.1 (fuente del tipo de cambio); P-07.2 (fecha del tipo de cambio); P-07.3 (tasa de IVA); P-07.4 (orden entre descuentos y conversión); P-07.5 (precio base con o sin IVA); P-07.6 (decimales en dólares); P-07.7 (otras monedas).

### RF-08 Generación de precios preliminares

**Descripción funcional**

Dado que los precios calculados requieren ser revisados antes de su autorización,  
cuando el usuario genere una propuesta de precios,  
entonces el sistema deberá generar la lista de precios con los resultados obtenidos a partir de las condiciones configuradas para poder aprobar. La lista nace con el estatus *Capturada* **[a validar: que la lista preliminar sea la lista en estatus Capturada]** y avanza por el flujo de estatus definido en el Contexto (C.5).

**Reglas de negocio vinculadas:** RN-010

**Criterios de aceptación**

CA-08.1 Dado que existen productos, clientes y condiciones configuradas para realizar un cálculo,  
cuando el usuario genere una propuesta de precios, entonces el sistema deberá crear una lista de precios preliminar con los precios calculados.

CA-08.2 Dado que una lista preliminar ha sido generada, cuando el usuario la consulte,  
entonces el sistema deberá identificarla con el estatus Capturada **[a validar: que la lista preliminar sea la lista en estatus Capturada]** y evitar que sus precios sean considerados como autorizados.

CA-08.3 Dado que una lista tiene un estatus del flujo, cuando avance en el proceso, entonces el sistema deberá seguir el orden Capturada, Pendiente Aprobar Dirección, Pendiente Aprobar Cliente, Pendiente Autorizar y Autorizada, y mostrar la lista en el cuadrante del Monitor que corresponde a su estatus.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-08.1 (clientes por lista, ver P-02.3); P-08.3 (estatus que permiten modificar); P-08.4 (conservación de listas Cancelada y No Autorizada); P-08.5 (botón Enviar a negociación); salidas a Cancelada y No Autorizada; significado de Pendiente Autorizar; columnas y acciones del Monitor; wireframe de la pestaña de salida (G-12); interpretación de que la lista preliminar es la lista Capturada (por confirmar).

### RF-09 Consulta y revisión de precios calculados

**Descripción funcional**

Dado que los precios calculados deben ser revisados por los responsables del proceso,  
cuando un usuario autorizado consulte la propuesta de precios, entonces el sistema deberá mostrar el detalle del cálculo, incluyendo cliente, producto, precio de referencia, condiciones aplicadas y precio resultante.

**Reglas de negocio vinculadas:** RN-005

**Criterios de aceptación**

CA-09.1 Dado que existe una lista de precios preliminar, cuando un usuario autorizado la consulte, entonces el sistema deberá mostrar el cliente, producto, precio de referencia, condiciones aplicadas y precio calculado.

CA-09.2 Dado que el usuario identifica una inconsistencia en un precio preliminar,  
cuando revise el detalle del cálculo, entonces deberá contar con la información necesaria para identificar el origen y las condiciones que generaron el resultado.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-09.1 (comparación con el precio vigente anterior); P-09.2 (columnas mínimas); P-09.3 (marcador Cadena distinta y contador Sin operaciones).

### RF-10 Validación y aprobación de precios

**Descripción funcional**

Dado que los precios calculados requieren autorización antes de ser utilizados comercialmente,  
cuando el usuario autorizado revise y apruebe la propuesta de precios, entonces el sistema deberá avanzar la lista por el flujo de estatus (Pendiente Aprobar Dirección, Pendiente Aprobar Cliente y Pendiente Autorizar) hasta cambiar el estado de los precios a autorizados y permitir su utilización en los procesos posteriores.

**Reglas de negocio vinculadas:** RN-007, RN-010

**Criterios de aceptación**

CA-10.1 Dado que una lista de precios se encuentra pendiente de revisión, cuando un usuario autorizado la valide y apruebe en cada paso del flujo (Dirección, Cliente y autorización final), entonces el sistema deberá cambiar su estatus al siguiente del flujo hasta llegar a Autorizada. **[a validar: responsable de cada paso]**

CA-10.2 Dado que una lista de precios no ha sido aprobada, cuando un usuario intente utilizarla comercialmente, entonces el sistema no deberá considerarla como una lista de precios autorizada.

CA-10.3 Dado que un precio ha sido aprobado, cuando se consulte su información, entonces el sistema deberá identificar al usuario y la fecha de aprobación.

CA-10.4 Dado que una lista avanza por el flujo de aprobación, cuando un usuario intente saltar un paso, entonces el sistema deberá impedirlo y conservar el orden definido (ver C.5).

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-10.1 (aprobador y papel del Enlace de Ventas); P-10.2 (niveles de aprobación); P-10.3 (rechazo); P-10.4 (lista completa o por clave); P-10.5 (notificación); P-10.6 (aprobación del Cliente); P-10.7 (paso Pendiente Autorizar a Autorizada).

### RF-11 Generación de lista de precios autorizada

**Descripción funcional**

Dado que los precios han sido revisados y aprobados,  
cuando concluya el proceso de aprobación,  
entonces el sistema deberá generar o actualizar la lista de precios correspondiente con los precios autorizados para el cliente y productos definidos.

**Reglas de negocio vinculadas:** RN-008, RN-010

**Criterios de aceptación**

CA-11.1 Dado que los precios de una propuesta han sido aprobados, cuando concluya el proceso de autorización, entonces el sistema deberá generar o actualizar la lista de precios correspondiente (la lista detallada vinculada) con los precios autorizados.

CA-11.2 Dado que una lista de precios ha sido autorizada, cuando un usuario consulte sus productos, entonces el sistema deberá mostrar los precios vigentes y aplicables al cliente correspondiente.

CA-11.3 Dado que la fecha de aprobación de una lista puede ser diferente a la fecha en que los precios deberán comenzar a aplicarse, cuando se genere o autorice la lista de precios,  
entonces el sistema deberá permitir capturar la fecha de vigencia a partir de la cual los precios autorizados podrán ser aplicados en el sistema, independientemente de la fecha en que se realizó la aprobación.

CA-11.4 Dado que una lista de precios puede dejar de ser aplicable antes o después de la fecha inicialmente establecida debido a la finalización de la relación comercial o a otra condición autorizada, cuando un usuario con los permisos correspondientes registre la fecha de finalización de vigencia, entonces el sistema deberá actualizar la vigencia de la lista y evitar que sus precios sean utilizados posteriores a dicha fecha.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-11.1 (lista nueva o actualizada); P-11.2 (momento de captura de la vigencia); P-11.3 (vigencias traslapadas); P-11.4 (fin anticipado de vigencia); P-11.5 (precio del Pedido de Venta sin lista vigente); P-11.6 (paso de carga en Auditoría de Ventas); P-11.7 (lista autorizada anterior).

### RF-12 Control de modificaciones

**Descripción funcional**

Dado que la configuración y los precios pueden requerir modificaciones, cuando un usuario autorizado realice un cambio sobre la información relacionada con la determinación de precios, entonces el sistema deberá registrar la modificación realizada para mantener el control y seguimiento del cambio.

**Reglas de negocio vinculadas:** RNF-04

**Criterios de aceptación**

CA-12.1 Dado que existe información configurada para la determinación de precios, cuando un usuario autorizado modifique dicha información, entonces el sistema deberá registrar el cambio realizado.

CA-12.2 Dado que se ha realizado una modificación, cuando un usuario consulte el historial de cambios, entonces el sistema deberá permitir identificar la información modificada, el usuario responsable y la fecha del cambio.

Responsable de validación: ( ) Cliente (x) Product Owner (x) Área de Negocio

**Dudas abiertas:** P-12.1 (entidades auditadas); P-12.2 (valor anterior y nuevo); P-12.3 (conservación y exportación); P-12.4 (auditoría de cambios de estatus).

### RF-13 Validaciones del proceso

**Descripción funcional**

Dado que el cálculo de precios requiere información y configuraciones previamente definidas, cuando el usuario intente ejecutar un cálculo con información obligatoria incompleta o inexistente, entonces el sistema deberá identificar la información faltante y evitar la ejecución del cálculo hasta que se cumplan las condiciones requeridas.

**Reglas de negocio vinculadas:** RN-001, RN-002

**Criterios de aceptación**

CA-13.1 Dado que existen datos obligatorios requeridos para realizar el cálculo, cuando el usuario intente ejecutar el proceso sin completar alguno de ellos, entonces el sistema deberá identificar la información faltante y mostrar un mensaje indicando que debe ser completada.

CA-13.2 Dado que no existe un precio de referencia o condición necesaria para realizar el cálculo,  
cuando el usuario intente ejecutar el proceso, entonces el sistema deberá impedir el cálculo y mostrar la condición que requiere atención.

CA-13.3 (nuevo, a validar) Dado que una clave especial no tiene clave comercial relacionada, cuando el usuario ejecute el cálculo, entonces el sistema no deberá bloquearlo por la falta de clave comercial, pero sí deberá bloquearlo y señalar la clave si le falta el precio inicial capturado a mano.

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

**Dudas abiertas:** P-13.1 (datos obligatorios por tipo de lista); P-13.2 (bloqueo o advertencia); P-13.3 (validaciones de coherencia); P-13.4 (validación del precio capturado a mano).

### RF-14 Control de acceso

**Descripción funcional**

Dado que las funcionalidades de gestión de precios requieren diferentes niveles de responsabilidad,  
cuando un usuario ingrese a las funcionalidades del proceso, entonces el sistema deberá permitir o restringir las acciones disponibles de acuerdo con el perfil y permisos asignados.

**Reglas de negocio vinculadas:** RNF-01

**Criterios de aceptación**

CA-14.1 Dado que el usuario tiene un perfil y permisos determinados, cuando ingrese al módulo de gestión de precios, entonces el sistema deberá mostrar únicamente las funcionalidades y acciones autorizadas para su perfil.

CA-14.2 Dado que un usuario no cuenta con permisos para modificar o aprobar precios, cuando intente realizar dicha acción, entonces el sistema deberá impedirla.

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

**Dudas abiertas:** P-14.1 (perfiles); P-14.2 (calcula y aprueba la misma persona); P-14.3 (restricción por cliente, región o lista); P-14.4 (perfil que cancela y desde qué estatus).

### RF-15 Historial de precios

**Descripción funcional**

Dado que los cálculos pueden requerir consultar precios de periodos anteriores, cuando un usuario autorizado consulte el historial de un precio o producto, entonces el sistema deberá permitir identificar los precios previamente determinados, su vigencia y la información asociada a su determinación.

**Reglas de negocio vinculadas:** RNF-04, RN-002

**Criterios de aceptación**

CA-15.1 Dado que existen precios determinados en periodos anteriores, cuando el usuario autorizado consulte el historial de un producto o cliente, entonces el sistema deberá mostrar los precios previamente determinados y su periodo de vigencia.

CA-15.2 Dado que un precio histórico puede utilizarse como referencia para un nuevo cálculo, cuando el usuario seleccione dicha referencia, entonces: el sistema deberá utilizar el precio correspondiente al periodo seleccionado.

CA-15.3 Dado que una lista de precios ha finalizado su vigencia, cuando un usuario consulte su historial, entonces el sistema deberá conservar y mostrar la información de la lista, incluyendo su periodo de vigencia y fecha de finalización, sin permitir su utilización para nuevas operaciones posteriores a dicha fecha.

Responsable de validación: ( ) Cliente (x) Product Owner ( ) Área de Negocio

**Dudas abiertas:** P-15.1 (datos del historial); P-15.2 (filtros y exportación); P-15.3 (CA-15.3 en RF-11 o aquí); P-15.4 (pestaña del Monitor frente al historial).

## 2.3 Requerimientos No Funcionales (si aplica)

|        |                              |                                                                                                                                                                                                                                                                                                                                                                     |                          |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| **ID** | **Nombre del Requerimiento** | **Descripción Funcional**                                                                                                                                                                                                                                                                                                                                           | **Tipo (Story/Feature)** |
| RNF-01 | Seguridad                    | El sistema deberá garantizar el acceso controlado a las funcionalidades de gestión de precios mediante perfiles y permisos, protegiendo la información, configuraciones, reglas y precios contra modificaciones o accesos no autorizados.                                                                                                                           | Product Backlog          |
| RNF-02 | Desempeño                    | El sistema deberá ejecutar las operaciones de consulta, cálculo y actualización de precios de manera eficiente, manteniendo tiempos de respuesta adecuados y resultados consistentes de acuerdo con las reglas y condiciones configuradas.                                                                                                                          | Product Backlog          |
| RNF-03 | Disponibilidad               | El sistema deberá mantener disponibles las funcionalidades e información de precios durante el horario operativo establecido y contar con mecanismos que permitan la recuperación de la información ante interrupciones del servicio.                                                                                                                               | Product Backlog          |
| RNF-04 | Trazabilidad                 | El sistema deberá mantener la trazabilidad de la determinación de precios, permitiendo identificar el cliente, producto, precio de referencia y su origen —lista base vigente, lista base histórica o captura manual—, reglas y condiciones aplicadas, resultado obtenido, modificaciones realizadas y usuarios responsables del cálculo, revisión y aprobación. | Product Backlog          |

## 2.4 Reglas de Negocio

|         |                                                                                                                                                                                                                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ID**  | **Regla de Negocio**                                                                                                                                                                                                                                                                                 |
| RN-001  | Cada clave especial (de cliente, autoservicio o exportación) se relaciona con una sola clave de producto comercial, que servirá como referencia para obtener el precio correspondiente. Una clave comercial puede tener varias claves especiales, incluso de un mismo cliente, y la relación se comparte entre clientes. Pueden existir claves especiales sin clave comercial relacionada: su precio inicial se captura a mano. |
| RN-002  | El cálculo del precio deberá partir de un precio inicial previamente definido, el cual provendrá de la lista base (A o B) vigente o histórica asignada a su clave comercial en el catálogo de claves, o de un precio inicial capturado a mano en las claves especiales sin clave comercial, según las condiciones comerciales establecidas. No existe precio calculado por cliente ni cadenas de referencia. |
| RN-003  | Cuando la presentación de la clave de producto del cliente sea diferente a la presentación de la clave comercial de referencia, el precio deberá ajustarse de manera proporcional mediante una fórmula parametrizable de la forma (v1 / v2) \* v3, cuyos valores introduce el usuario, con base en el número de piezas o kilos indicado en el catálogo de productos. El resultado se redondea a 2 decimales. |
| RN-004  | Al precio determinado mediante la proporcionalidad correspondiente se deberán aplicar los descuentos y sobreprecios establecidos, los cuales podrán definirse como importe, porcentaje o importe determinado a partir de una cantidad monetaria relacionada con el cubicaje de la clave de producto. |
| RN-005  | El precio de venta deberá resultar de la aplicación de las condiciones de proporcionalidad, descuentos y sobreprecios que correspondan a cada clave de producto y cliente.                                                                                                                           |
| RN-006  | Para las operaciones de exportación, el precio determinado deberá considerar el desglose del IVA y posteriormente convertirse a dólares utilizando el tipo de cambio definido para la determinación del precio.                                                                                      |
| RN-007  | Los precios calculados deberán ser revisados por el departamento de Ventas y avanzar por el flujo de estatus (aprobación de Dirección, aprobación del Cliente y autorización) antes de ser considerados como precios autorizados. **[a validar: responsable de cada paso]** |
| RN-008  | Una vez aprobados los precios, deberá generarse la lista de precios correspondiente con los precios autorizados.                                                                                                                                                                                     |
| RN-009  | El tipo de lista (Especial Cliente, Autoservicio o Exportación) acota las claves de producto que se pueden agregar a la lista: cada tipo utiliza su clase de clave. También acota las listas de referencia utilizables, que deberán ser del mismo tipo **[a validar]**. |
| RN-010  | Toda lista de precios personalizada nace con el estatus Capturada y avanza en este orden: Pendiente Aprobar Dirección, Pendiente Aprobar Cliente, Pendiente Autorizar y Autorizada. Al llegar a Autorizada la lista sale de los cuadrantes del Monitor. |
| RN-011  | La lista base (A o B) de cada clave comercial se define en el catálogo de claves y no al configurar la lista de precios. |

**Nota: - Estas reglas pueden trasladarse como Criterios de Aceptación en los product backlogs / historias de usuario en Azure DevOps.**

# 3. Criterios de Aceptación

\[Indicar cómo y quién validará que el requerimiento fue cumplido (Condiciones medibles y comprobables\]

Los criterios de aceptación de cada requerimiento (CA-xx.x) y el responsable de su validación se encuentran en la ficha de cada RF de la sección 2.2.

# 4. Supuestos y consideraciones

**Dependencias de negocio/proceso**

- El departamento de **Ventas** deberá proporcionar y validar las condiciones comerciales, reglas de cálculo, productos y relaciones entre claves requeridas para la determinación de precios.

- Los precios calculados deberán ser revisados por **Ventas** y aprobados por los usuarios definidos para este proceso.

- Las fechas de inicio y fin de vigencia de las listas de precios deberán ser definidas por el área responsable, considerando la vigencia de las condiciones comerciales y, cuando corresponda, la finalización de la relación comercial con el cliente.

- Las listas que finalicen su vigencia deberán conservarse como información histórica y no deberán eliminarse.

**Información de entrada requerida**

- Clientes y listas de precios correspondientes.

- Claves de producto del cliente y claves comerciales de referencia.

- Presentaciones de producto, piezas o kilos requeridos para determinar la proporcionalidad.

- Precios de referencia y su origen.

- Descuentos, sobreprecios y demás condiciones comerciales aplicables.

- Información requerida para operaciones de exportación, incluyendo tipo de cambio.

- Fechas de inicio y fin de vigencia de las listas de precios.

**Dependencias técnicas**

- Disponibilidad y consistencia de la información maestra de **clientes, productos y listas de precios** en R1.

- Disponibilidad de la estructura requerida para configurar las reglas y condiciones que intervienen en el cálculo.

- Capacidad de R1 para conservar el historial de precios, vigencias y trazabilidad de las operaciones.

- Disponibilidad del mecanismo requerido para obtener el tipo de cambio utilizado en los cálculos de exportación.

**Integraciones involucradas**

- **Gestión de Ventas – Pedido de Venta**, para la aplicación del precio autorizado y vigente de acuerdo con el cliente y producto.

**Grupos de usuarios afectados**

- **Gerentes de Ventas:** configuración de condiciones comerciales, generación, revisión y gestión de listas de precios.

- **Enlaces de Ventas** revisión y aprobación de precios.

**Riesgos operativos asociados**

- Información o condiciones comerciales incorrectas o incompletas que generen un cálculo de precio incorrecto.

- Definición incorrecta de las fechas de vigencia, ocasionando la aplicación de precios fuera del periodo autorizado.

- Diferencias entre la información utilizada actualmente en Excel y la información configurada en R1 durante la implementación.

- Cambios en las condiciones comerciales que no se encuentren contemplados en las reglas configuradas.

## 4.1 Flujo Funcional / Proceso (si aplica)

![](media/media/image3.png)

![](media/media/image4.png)

![](media/media/image5.png)

## 4.2 Diseño Funcional (Wireframes / Mockups si aplica)

| Pantalla 1. Cotización de Lista de precios![](media/media/image6.png) | En esta pantalla se podrá configurar: nombre, tipo de lista, vigencia, lista base para el precio, lista detallada a la que se aplicará, claves de producto del cliente. Se podrá visualizar la configuración entre la clave de producto del cliente y la clave de producto comercial equivalente, así como el precio base referenciado. También se podrá visualizar el precio determinado al cliente con base en las operaciones del cálculo de precios. Desde ahí se podrá pasar a la pantalla donde se configuraron. En el Contexto (C.4) esta pantalla se denomina temporalmente *Cotizador de Lista de Precios Personalizada*. |
|-------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pantalla 2. Agregar operaciones ![](media/media/image7.png)           | En esta pantalla se podrá seleccionar la forma de aplicación de los parámetros de descuento, así como de sobreprecios que afectaran a las claves de producto del cliente. Mostrando el orden de aplicación según haya capturado el usuario autorizado.                                                                                                                                                                                                                                                                 |
| Pantalla 3. Operaciones ![](media/media/image8.png)                    | En esta pantalla se podrá visualizar los cálculos efectuados por el sistema con base en los parámetros configurados en la imagen anterior.                                                                                                                                                                                                                                                                                                                                                                             |
| Pantalla 4. Monitor de Lista de Precios Personalizadas (imagen por incorporar) | Pantalla principal de seguimiento del ciclo de vida de las listas, dividida en cuadrantes por estatus (ver C.6). Desde ahí se llama al Cotizador para agregar o modificar listas, y se autorizan o cancelan listas. Incluirá una pestaña para las listas Autorizada, Cancelada y No Autorizada (sin wireframe todavía). |

# 5. Capacitación (si aplica)

## 5.1 Impacto Organizacional y Requerimientos de Capacitación

La implementación del proyecto generará cambios en el proceso actual de determinación y gestión de precios, al trasladar al sistema R1 actividades que actualmente se realizan mediante archivos de Excel.

Las principales áreas, roles y componentes funcionales impactados serán:

- **Ventas:** será el principal grupo impactado, debido a que deberá gestionar en R1 la configuración de condiciones comerciales, generación y revisión de cálculos, listas preliminares, precios autorizados y vigencias.

- **Enlaces de Ventas:** será impactada en el proceso de revisión y aprobación de los precios antes de su aplicación comercial.

Los principales componentes funcionales impactados serán la **configuración y gestión de listas de precios personalizadas, cálculo de precios, revisión y aprobación, control de vigencias, consulta histórica y generación de lista detallada para la aplicación de precios en el Pedido de Venta**.

Será necesario realizar capacitación a los usuarios involucrados para asegurar la correcta adopción de la nueva funcionalidad y la transición del proceso actual basado en Excel hacia la gestión sistematizada en R1.

Se deberá generar **material de capacitación y apoyo operativo**, incluyendo una guía de uso de las funcionalidades implementadas y ejemplos del flujo de gestión de precios, considerando los escenarios de listas especiales, autoservicio y exportación.

## 5.2 Áreas y Roles impactados

| **Área** | **Rol**            | **Tipo de Usuario** | **Capacitación Requerida** |
|----------|--------------------|---------------------|----------------------------|
| Ventas   | Gerentes de Ventas | Operativo           | Sí                         |
| Ventas   | Enlaces de Ventas  | Aprobador           | Sí                         |

## 5.3 Componentes funcionales que requieren material de capacitación

| Módulo | Proceso | Pantalla / Catálogo | Tipo de Cambio<br>(Nuevo / Modificación)  | Cantidad de capital Humano |
|---|---|---|---|---|
|  |  |  |  |  |

## 5.4 Riesgos e Impactos Identificados

|           |                                                                                                                                                                                                      |                                                                                                                                                                                                                                 |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo      | Descripción                                                                                                                                                                                          | Mitigación                                                                                                                                                                                                                      |
| Operativo | La falta de capacitación de los usuarios podría ocasionar errores en la configuración, revisión, aprobación y gestión de las listas de precios.                                                      | Capacitar a los usuarios involucrados y proporcionar material de apoyo para el uso de las funcionalidades implementadas.                                                                                                        |
| Operativo | La falta de validación de los cálculos podría generar diferencias entre los precios obtenidos en R1 y los calculados actualmente mediante Excel.                                                     | Realizar pruebas comparativas con Ventas, validar los resultados y corregir las diferencias identificadas antes de la puesta en operación.                                                                                      |
| Técnico   | La información incompleta o inconsistente de claves de producto y condiciones de cálculo podría impedir la determinación correcta de los precios.                                                    | Documentar y validar las reglas de negocio con Ventas y comparar los resultados del sistema contra los cálculos actuales antes de su puesta en operación.                                                                       |
| Técnico   | La falta de disponibilidad o actualización del tipo de cambio podría afectar la determinación de los precios de exportación.                                                                         | Definir y validar el mecanismo de obtención o actualización del tipo de cambio, así como los controles para verificar su disponibilidad y vigencia.                                                                             |
| Negocio   | La falta de actualización de las condiciones comerciales o una definición incorrecta de las vigencias podría ocasionar la aplicación de precios que no correspondan a los acuerdos con los clientes. | Establecer responsables para proporcionar, validar y mantener actualizadas las condiciones comerciales utilizadas en los cálculos e implementar validaciones para aplicar únicamente precios autorizados dentro de su vigencia. |
| Negocio   | Los retrasos en la revisión y aprobación de precios podrían afectar la disponibilidad oportuna de las listas para la operación comercial.                                                            | Definir responsables y tiempos de atención para la revisión y aprobación de precios, así como dar seguimiento a las listas pendientes.                                                                                          |

# 6. Aprobaciones

**Mediante la firma del presente documento, el usuario solicitante manifiesta haber revisado y validado el contenido del Documento de Requerimientos del Sistema, confirmando que los requerimientos, alcances, funcionalidades y consideraciones aquí descritas reflejan de manera correcta sus necesidades y expectativas. Asimismo, acepta que este documento servirá como base para las actividades de análisis, diseño, desarrollo e implementación de la solución tecnológica correspondiente.**

|                                                 |                 |                  |           |
|-------------------------------------------------|-----------------|------------------|-----------|
| **Área**                                        | **Nombre**      | **Firma / VoBo** | **Fecha** |
| Usuario que solicita                            |                 |                  |           |
| Consultor (Product Owner)                       | Montserrat Mata |                  |           |
| Coordinador de Desarrollo                       | Miguel Lucio    |                  |           |
| Aseguramiento de Calidad de Software (opcional) | Eleazar Rosas   |                  |           |

# 7. Control de Cambios

|             |                |                            |                 |
|-------------|----------------|----------------------------|-----------------|
| **Versión** | **Fecha**      | **Descripción del Cambio** | **Autor**       |
| v1.0        | \[02/10/2026\] | Creación del documento     | Montserrat Mata |
| v1.1        | \[Fecha\]      | Ajustes por validación     |                 |
| v0.2        | 26/10/2026     | Versión derivada de la 0.1. Incorpora la sección Contexto y las respuestas de la PO: claves especiales y su relación con la clave comercial, listas base A y B, Cotizador, Monitor, estatus y flujo, precio inicial y fórmula de proporcionalidad. Reescribe RF-01 a RF-04, RF-08 y RF-10, ajusta RF-11 y RF-13, y actualiza RN-001 a RN-003, RN-007 y RNF-04. Agrega RN-009 a RN-011 y la sección 9 de dudas pendientes. Corrige el espacio en RN-006 y retira la instrucción de plantilla de 4.1. Unifica las secciones 2.2 y 3: la 2.2 queda como tabla índice más una ficha por RF (descripción, reglas vinculadas, criterios de aceptación, responsable de validación y dudas abiertas) y la sección 3 remite a esas fichas | Por definir     |

# 8. ANEXOS (Opcional)

- Minutas de sesión

- Evidencia de validación

- Correos de aprobación

- Documentos complementarios

# 9. Dudas pendientes

Preguntas aún abiertas para continuar el análisis. Los IDs corresponden al informe de validación DoR + INVEST (v3). Las dudas de aprobación, tipo de cambio e IVA y cálculo de operaciones (*criterio*) son las que más bloquean el paso a análisis técnico.

## 9.1 Prioritarias (bloquean el análisis técnico)

**Aprobación (RF-10, RF-14)**
- **P-10.1** ¿Aprueba el Enlace de Ventas o Dirección? ¿O los dos, en secuencia? El flujo confirma un paso de Dirección y después uno de Cliente; falta el papel del Enlace de Ventas.
- **P-10.6** ¿Qué es la *aprobación del Cliente*: la confirma una persona del cliente o un responsable interno que registra la conformidad del cliente?
- **P-10.7** ¿Quién ejecuta el paso *Pendiente Autorizar → Autorizada* y qué lo distingue de las dos aprobaciones anteriores?
- **P-10.3** Al rechazar, ¿el motivo es obligatorio? ¿La lista regresa a *Capturada* o queda en *No Autorizada*?

**Exportación (RF-07)**
- **P-07.1** ¿De dónde sale el tipo de cambio (catálogo de R1, captura manual, fuente externa)? ¿Quién lo actualiza y con qué frecuencia?
- **P-07.2** ¿Qué fecha de tipo de cambio se usa: la del cálculo, la de inicio de vigencia u otra?
- **P-07.3** ¿Qué tasa de IVA se desglosa? ¿Varía por cliente o región?
- **P-07.4** Los descuentos y cargos de RF-05, ¿se aplican antes de convertir (en pesos) o después (en dólares)?
- **P-07.5** ¿El precio base de las listas de exportación incluye IVA?
- **P-07.6** ¿Cuántos decimales lleva el precio en dólares y cómo se redondea?
- **P-07.7** ¿Hay clientes de exportación con una moneda distinta al dólar?

**Cálculo: proporcionalidad, descuentos y sobreprecios (RF-04, RF-05, RF-06)**
- **P-04.5** ¿Qué representan v1, v2 y v3? ¿Pueden tomarse del catálogo o siempre se capturan?
- **P-04.6** ¿La fórmula es siempre de la forma (v1 / v2) \* v3, o el usuario puede armar otras? ¿Dónde se captura y se guarda con la lista?
- **P-04.7** ¿Qué pasa si la clave comercial se calcula por piezas y la clave especial por kilos (o al revés)?
- **P-04.4 (parcial)** El redondeo es a 2 decimales. ¿Aplica solo al resultado final de la fórmula o también a pasos intermedios? (Se une a P-06.2).
- **P-05.1** ¿Las operaciones son solo las 4 de la pantalla 2 (Presentación Cliente, Cargo Logística, Cargo Publicidad y Descuento Pactado) o hay más?
- **P-05.2** ¿Qué significan las fuentes *Calculado*, *Guardado* y *Fijo*? ¿Dónde se guarda el *"valor de la clave"* de Cargo Publicidad?
- **P-05.3** ¿Qué es el cubicaje y de dónde sale? El costo de flete, ¿es por lista, por cliente o global?
- **P-05.4** ¿El orden lo define el usuario por clave? ¿Hay un orden obligatorio?
- **P-05.5** ¿Cada porcentaje se aplica sobre el precio acumulado (como en la pantalla 3) o sobre el precio base?
- **P-05.6** La opción de aplicar a una *categoría de producto*, ¿usa una categoría que ya existe en R1?
- **P-05.7** En el mapa mental, sobreprecios y descuentos tienen una opción *Criterio*. ¿Qué es un criterio?
- **P-05.8** El mapa mental no trae descuento en porcentaje, pero la pantalla 2 trae *Descuento Pactado en %*. ¿Los descuentos en porcentaje existen?
- **P-06.1** ¿Es correcto el orden: precio inicial, proporcionalidad, operaciones, y en exportación IVA y conversión?
- **P-06.2** ¿Cómo se redondea el precio final y los pasos intermedios?

## 9.2 Por RF y por tema

**Ciclo de vida, estatus y Monitor (RF-08, Contexto C.5 y C.6)**
- Salidas a *Cancelada* y *No Autorizada*: desde qué estatus se puede pasar, quién lo decide y qué pasa con una lista rechazada.
- Qué representa el estatus *Pendiente Autorizar* frente a los de Dirección y Cliente (el orden ya está definido).
- Wireframe de la pestaña del Monitor con las listas *Autorizada*, *Cancelada* y *No Autorizada* (G-12).
- Qué columnas del Monitor aplican a listas de precios (Pedido, Piezas, Kilos, Fecha Carga y Fecha Entrega parecen heredadas de un monitor de pedidos) y cuáles de sus acciones aplican.
- **P-08.1** (parcial) ¿Una lista pertenece a uno o a varios clientes? (Ver P-02.3.)
- **P-08.3** (parcial) ¿En qué estatus se permite modificar una lista?
- **P-08.4** (parcial) ¿Cuánto tiempo se conservan las listas *Cancelada* y *No Autorizada*?
- **P-08.5** ¿El botón *"Enviar a negociación"* del wireframe es el que pasa la lista a *Pendiente Aprobar Cliente*, o ese paso es automático?
- Interpretación por confirmar: que la lista preliminar sea la lista en estatus *Capturada*.

**RF-01 Claves de producto**
- **P-01.1 (parcial)** ¿Esas varias claves especiales de un mismo cliente corresponden a presentaciones distintas del mismo producto?
- **P-01.4 (parcial)** El precio inicial de las claves sin clave comercial se captura a mano. ¿Después siguen el cálculo completo (proporcionalidad, descuentos y sobreprecios) o ese precio ya es el final? ¿Cómo se identifican en la revisión (RF-09) y en la aprobación (RF-10)?
- **P-01.5** En el mapa mental, la lista de Exportación apunta a *Clave Exportación* y también a *Clave Especial Cliente*. ¿Esa flecha sobra?
- **P-01.6** Como la relación clave especial - clave comercial se comparte entre clientes, ¿quién puede modificarla o eliminarla y cómo se evita que un cambio afecte listas ya autorizadas?

**RF-02 Listas de precios (Cotizador)**
- **P-02.1 (parcial)** Los tres tipos de lista usan todos los campos del Cotizador. ¿Todos son obligatorios? Algunos parecen no serlo (*Observaciones*, *Lista detallada ref.*, la clave comercial en claves sin clave comercial); el estatus y el identificador los asigna el sistema.
- **P-02.3 (parcial)** ¿El cliente de referencia es el de la lista detallada de referencia (en el wireframe, *LD-0123 · Cliente A*)? ¿Debe estar incluido en el listado? ¿Una lista puede tener cero clientes antes de aprobarse?
- **P-02.5** ¿Se puede entregar primero solo la lista Especial? (Ver G-9.)
- **P-02.8 (interpretación por confirmar)** La PO respondió "sí". Se interpretó como que una lista solo puede tomar como referencia otra lista del mismo tipo.
- **P-02.10** ¿Cómo se identifica una nueva versión de una lista: mismo identificador con número de versión, o identificador nuevo? ¿La versión anterior queda vigente, vencida o cancelada al autorizarse la nueva?
- **P-02.11** Al crear una nueva versión, ¿se copian las claves, operaciones y clientes de la versión anterior?
- Si una clave comercial no tiene lista base (A o B) asignada en el catálogo de claves, ¿qué hace el sistema? (Se relaciona con RF-13.)

**RF-03 Precio de referencia**
- **P-03.6** Si el origen puede ser general o por clave, ¿qué prevalece si hay uno por clave y otro general? ¿Se agrega al wireframe un campo de fuente por clave? ¿Cómo se elige una lista histórica (por fecha o por identificador)?

**RF-06 Cálculo**
- **P-06.3** ¿Cuándo se recalcula (al cambiar el precio base, una operación o la lista base)? ¿Un recálculo obliga a revisar de nuevo?
- **P-06.4** ¿Una clave con *"Sin operaciones"* es válida? ¿Su precio final es el precio base?
- **P-06.5** ¿Se puede recalcular una lista en cualquier estatus o solo mientras está *Capturada*? Si ya pasó a Dirección y se recalcula, ¿regresa a *Capturada*?

**RF-09 Consulta y revisión**
- **P-09.1** ¿La revisión necesita comparar contra el precio vigente anterior, o con ver el desglose es suficiente?
- **P-09.2** ¿Qué columnas mínimas debe tener la vista de revisión?
- **P-09.3** ¿Qué significan el marcador *"Cadena distinta"* y el contador *"Sin operaciones"* del wireframe y deben formar parte de la revisión?

**RF-10 Aprobación (otras)**
- **P-10.2** ¿Hay niveles de aprobación según monto o variación de precio?
- **P-10.4** ¿Se aprueba la lista completa o clave por clave?
- **P-10.5** ¿El sistema debe notificar al aprobador (correo u otro aviso) o basta con el Monitor?

**RF-11 Lista autorizada y vigencia**
- **P-11.1** ¿Se genera una nueva lista detallada o se actualiza la existente? (La PO confirmó que la lista detallada vinculada es la de R1 que se actualiza al autorizar; falta definir el caso de una nueva versión.)
- **P-11.2** (parcial) Las fechas de vigencia forman parte de los datos del Cotizador; ¿se pueden ajustar al autorizar? Hoy CA-11.3 las ubica al autorizar.
- **P-11.3** ¿Se permite que un cliente tenga dos listas vigentes del mismo tipo con fechas traslapadas?
- **P-11.4** El fin anticipado de vigencia, ¿quién lo registra y con qué motivo?
- **P-11.5** ¿Qué precio toma el Pedido de Venta si la lista venció o no hay lista vigente?
- **P-11.6** Hoy Ventas manda la lista a Auditoría de Ventas para cargarla. ¿Ese paso desaparece?
- **P-11.7** Cuando una lista nueva pasa a *Autorizada*, ¿qué pasa con la lista autorizada anterior del mismo cliente y tipo?

**RF-12 Control de modificaciones**
- **P-12.1** ¿Qué entidades deben auditarse (claves, listas, referencias, operaciones, tipo de cambio, precios, aprobaciones)?
- **P-12.2** ¿Se registra valor anterior y valor nuevo, o solo quién y cuándo?
- **P-12.3** ¿Cuánto tiempo se conserva y se debe poder exportar?
- **P-12.4** ¿Se audita cada cambio de estatus de la lista (incluidas *Cancelada* y *No Autorizada*) con el usuario que lo ejecutó?

**RF-13 Validaciones**
- **P-13.1** ¿Qué datos son obligatorios en cada tipo de lista?
- **P-13.2** ¿Todas las validaciones bloquean el cálculo o algunas solo advierten?
- **P-13.3** ¿Hay validaciones de coherencia (precio menor o igual a cero, descuento mayor a 100%, variación excesiva contra el precio anterior)?
- **P-13.4** El precio inicial capturado a mano en claves sin clave comercial, ¿tiene alguna validación o se acepta tal cual?

**RF-14 Control de acceso**
- **P-14.1** ¿Qué perfiles existen en R1 y cuáles se usan aquí (Gerente de Ventas, Enlace de Ventas, Dirección, Auditoría de Ventas, Administrador)?
- **P-14.2** ¿Quien calcula puede ser también quien aprueba?
- **P-14.3** ¿Hay restricción por cliente, región o lista?
- **P-14.4** Desde el Monitor se puede autorizar y cancelar. ¿Qué perfil cancela una lista y desde qué estatus?

**RF-15 Historial**
- **P-15.1** ¿Qué datos debe mostrar el historial por precio?
- **P-15.2** ¿Con qué filtros se consulta y se necesita exportarlo?
- **P-15.3** CA-15.3 (fin de vigencia), ¿se queda aquí o se consolida con RF-11?
- **P-15.4** La pestaña del Monitor con listas *Autorizada*, *Cancelada* y *No Autorizada*, ¿es el historial de este RF o es una consulta distinta?

**Mapa mental**
- Qué es un *criterio* (P-05.7) y si existe descuento en porcentaje (P-05.8).

## 9.3 Generales del documento

- **G-1** ¿Quién es el responsable del requerimiento y quién firma como usuario que solicita?
- **G-2** ¿Cuál es la versión vigente (0.1 o 1.0) y la fecha de elaboración correcta (01/01/2026 o 02/10/2026)?
- **G-3** ¿Cuántos clientes, claves por lista, listas y usuarios simultáneos se esperan?
- **G-4** ¿Cuál es el horario operativo que debe cubrir la disponibilidad (RNF-03) y qué tiempos de respuesta se esperan (RNF-02)?
- **G-5** ¿Se puede compartir un Excel actual de cada tipo de lista (especial, autoservicio, exportación) con un cálculo completo, para usarlo como caso de prueba?
- **G-6** ¿Hay fecha límite o un evento de negocio que defina la prioridad Alta?
- **G-7** La integración con el Pedido de Venta, ¿es solo de lectura del precio autorizado o el pedido escribe algo de vuelta?
- **G-8 (parcial)** La carga inicial de claves entra al alcance (campo nuevo en las cargas Excel). Falta definir la carga de precios.
- **G-9** ¿Se puede entregar primero la lista Especial y dejar Autoservicio y Exportación para una segunda entrega?
- **G-10** ¿Hay alguna cifra del problema actual (horas por ciclo de cálculo, errores detectados) para cuantificar el beneficio?
- **G-11** El proyecto generará varias pantallas de trabajo. Además del Cotizador y del Monitor, ¿cuáles otras? ¿Entrarán como RF nuevos?
- **G-12** Wireframe de la pestaña del Monitor con las listas *Autorizada*, *Cancelada* y *No Autorizada*.
- Tabla 5.3 (Componentes funcionales que requieren material de capacitación) sin llenar.
