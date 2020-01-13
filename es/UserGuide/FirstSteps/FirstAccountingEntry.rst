.. highlight:: rst
.. title:: Facturascripts primeros pasos: Tu primer asiento contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Primeros pasos. Como crear asientos contables en FacturaScripts 2020.
  :keywords: facturascripts, configurar, dar de alta, asientos, asientos contables
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Primer Asiento FacturaScripts 2020
  :lang: es

#################
Tu primer asiento
#################

Después de dar sus primeros pasos en Facturascripts, ha llegado la hora de crear su primer asiento.
Para ello dirígase al menú (:guilabel:`Contabilidad->Asientos contables`).

Nos encontramos con tres pestañas de menú:

:Asientos contables: Visualiza la lista de asientos y permite la edición, edición y borrado de los mismos.
:Conceptos predefinidos: Relación de conceptos automáticos que sirven de ayuda en la entrada de nuevos asientos.
:Diarios: Conjunto de libros de diario de asientos de las empresas. Permiten agrupar los asientos por distintos conceptos o asignaciones.

Si partes de una nueva instalación (sin datos), la pestaña de *Asientos contables* y *Conceptos predefinidos* estarán vacías.

Diarios
=======

Al instalar la aplicación se crean cuatro diarios predefinidos: *Principal*, *Diario de facturas*, *Cartera de pagos* y *Cartera de cobros*.
Puede crear tantos como necesite pulsando el botón nuevo (+ con fondo verde), y rellenando los campo:

:Código: Identificador interno del diario.
:Descripción: Identificador para el usuario del diario.


Conceptos predefinidos
======================

Al introducir nuevos asientos, introducimos un concepto que identifica el asiento.
Estos conceptos suelen repetirse, de forma completa o parcialmente. Podemos dar de alta aquellos conceptos que vamos
a utilizar con más asiduidad mediante el botón verde con el signo [+]. Rellenaremos los datos del formulario:

:Código: Identificador interno del concepto.
:Descripción: Texto base que se usará para crear el concepto del asiento.

En el campo *Descripción* podemos hacer uso de comodines o expresiones que se sustituirán por el valor correspondiente
en el momento de usarse en la entrada de asientos. Los comodines que podemos usar son:

-   **%document%**: Se sustituirá por el valor del documento indicado en la cabecera del asiento contable.
-   **%date%**: Se sustituirá por la fecha actual (fecha del ordenador).
-   **%date-entry%**: Se sustituirá por la fecha del asiento contable.
-   **%month%**: Se sustituirá por el mes actual (de la fecha actual).
-   **%year%**: Se sustituirá por el año actual (de la fecha actual).

Ejemplo:

.. code:: text

    Descripción: S/Fra. %document%
    Descripción: Nómina del mes de %month%
    Descripción: Doc. %document% pagado el %date-entry%


Asientos Contables
==================

En la pestaña Asientos contables hacemos click sobre el botón nuevo (+ con fondo verde).
Creamos los Datos generales del asiento, como:

:Ejercicio: En el menú desplegable seleccionamos el ejercicio correspondiente al asiento a realizar. Lo normal es que sea el ejercicio en curso.
:Fecha: Seleccionamos la fecha del asiento contable.
:Diario: En el menú desplegable seleccionamos el Diario correspondiente al asiento que vamos a realizar.
:Canal: Agrupación que permite la emisión posterior de informes analíticos por distintos conceptos.
:Concepto: Descripción del asiento contable.
:Documento: Identidicador del documento al que hace referencia la operación del asiento.

Pulsamos *Guardar* para aceptar los datos de la cabecera del asiento, momento en el que se refrescará la pantalla
accediendo al asiento contable con la cabecera del asiento ya completa y una vista inferior para la introducción
de las partidas contables. La información de la cabecera del asiento se puede modificar posteriormente.

En la zona de las partidas podemos rellenar las líneas correspondientes, indicando la subcuentas, pudiendo elegir de la lista desplegable,
la contrapartida, la descripción o concepto de la línea e importe en el Debe o en el Haber. Las descripciones o conceptos de las partidas se pueden elegir de la lista desplegable, en base a los conceptos predefinidos
creados con anterioridad.

El grid de líneas de asiento se puede editar como si fuesen filas de una hoja de cálculo, insertando anterior y posteriormente nuevas líneas, moviéndolas, eliminarlas, copiar y pegar, etc.
Cuando tengamos nuestro asiento finalizado pulsamos guardar para guardar cambios.

.. nota::
    Si quiere importar un plan de cuentas puede consultar la sección de documentación (:guilabel:`Configuración->Plan de cuentas`).
