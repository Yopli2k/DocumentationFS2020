.. highlight:: rst
.. title:: Regularización Contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Proceso de regularización contable.
  :keywords: facturascripts, regularizacion, contabilidad, AccountingClosingRegularization
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Regularización Contable
  :lang: es


###############################
AccountingClosingRegularization
###############################

Esta clase, que hereda de *AccountingClosingBase*, realiza todo el proceso
de regularización del ejercicio contable. Esto significa que traspasa los
saldos de las subcuentas de compras y ventas a la cuenta de pérdidas y ganancias.

Al iniciar el proceso, se comprueba que exista alguna cuenta o subcuenta
con el tipo especial **PYG** en caso contrario se cancela el proceso y se
muestra un mensaje de error. La cuenta de pérdidas y ganancias donde se
contabilizará se guarda en la propiedad **subAccount** de la clase. También,
como parte del proceso inicial, se elimina cualquier asiento de regularización
ya existente dentro del ejercicio.

El asiento que se crea tiene asignado el tipo de operación 'R' que lo identifica
como asiento de regularización.


Métodos principales
===================

La clase puede ser llamada utilizando el método **exec**, informando del ejercicio
y el identificador del diario, para crear el asiento o con el método **delete**, informando
del ejercicio donde se ha de eliminar el asiento.

El parámetro de ejercicio es un objeto del modelo *Ejercicio* con los datos del ejercicio
donde se realiza o se elimina la regularización.


Métodos GET
===========

Estos métodos son llamados para obtener información sobre la regularización.

:getConcept: Retorna el concepto para el asiento y sus líneas. Por defecto 'Regularización del ejercicio' más el nombre del ejercicio.

:getDate: Retorna la fecha establecida como fecha fin del ejercicio.

:getOperation: Retorna el valor *R*.

:getSubAccountsFilter: Retorna la condición where para filtrar las subcuentas entre el grupo **6** y **7**


Métodos SET
===========

Estos métodos se utilizan para establecer datos generales o por defecto.

:setDataLine: Además de asignar los valores por defecto de la línea de asiento, establece los importes del debe y haber.


Métodos SAVE
============

:saveBalanceLine: Graba en el asiento la línea de pérdidas y ganancias.


Otros métodos
=============

Para el proceso de búsqueda y carga de los datos de la subcuenta de pérdidas y ganancias
esta clase implementa el método **loadSubAccount**.
