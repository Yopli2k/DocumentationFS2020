.. highlight:: rst
.. title:: Facturascripts configurar: Impuestos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Configurar impuestos en FacturaScripts 2020.
  :keywords: facturascripts, configurar, impuestos
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Configurar Impuestos FacturaScripts 2020
  :lang: es

#########
Impuestos
#########

Para empezar a realizar documentos de compra o de venta es necesario establecer los distintos tipos
y porcentajes de impuestos a aplicar. Para este efecto debemos ir a la opción del menú
(:guilabel:`Contabilidad->Impuestos->Impuestos`). Por defecto están los tipos de IVA vigentes para España.
En la actualidad existen cuatro tipos distintos:

    - IVA General: 21%
    - IVA Reducido: 10%
    - IVA Súper reducido: 4%
    - IVA Actividades exentas: 0%

Para crear un nuevo tipo de impuesto debemos hacer clic en el botón de insertar (botón con fondo verde
y signo *+*) y rellenamos los campos del formulario.

:Código: Identificador interno para el impuesto. Debe ser único. No puede repetirse
:Descripción: Texto que describe y ayuda al usuario a su identificación
:% IVA: Porcentaje de impuesto a aplicar
:% R.E.: *(% Recargo de Equivalencia)* Porcentaje adicional que se aplica al impuesto


Zonas de impuestos
==================

Al configurar las zonas de impuestos, automáticamente asignaremos un tipo impositivo distinto en función del país
o provincia del cliente. Para acceder a la configuración de zona de impuestos debemos ir a la opción del menú
(:guilabel:`Contabilidad->Impuestos->Impuestos`) en la pestaña *Zonas de impuestos*.

Podremos asignar la exención de las facturas emitidas a empresas y profesionales intracomunitarias, ventas a
particulares de países de la UE con un tipo impositivo distinto al general español, etc.

Para crear una exención de impuesto basta con hacer clic en el botón de insertar (botón con fondo verde y signo *+*) y
rellenamos los campos del formulario.

:Impuesto: Seleccionamos de la lista el impuesto al que deseamos aplicar la excepción
:País: Indica a que país se aplica la excepción. "*-*" para todos los países
:Provincia: Indica a que provincia se aplica la excepción. "*-*" para todas las provincias
:I. Aplicado: *(Impuesto Aplicado)* Seleccionamos el impuesto que deseamos aplicar
:Prioridad: Establece el órden de prioridad, para casos en los que existan varias excepciones concurrentes

Este procesora se repetira en todos los impuesos que queramos crear exenciones.

**Ejemplo**:

Deseamos quitar el 21% de IVA (general) de España, en las provincia de Las Palmas,
Santa Cruz de Tenerife, Ceuta, Melilla.
Para el resto de provincias Españolas se aplicará el 21% de IVA.


.. note::
    Las zonas de impuesto se filtran por el orden de prioridad, donde 100 es la máxima prioridad y
    va perdiendo valor conforme se reduce el número.
