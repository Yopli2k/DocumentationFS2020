.. highlight:: rst
.. title:: Cierre Contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Proceso de cierre contable.
  :keywords: facturascripts, cierre, contabilidad, Cierre Contable
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Cierre Contable
  :lang: es


########################
AccountingClosingClosing
########################

Esta clase, que hereda de *AccountingClosingBase*, realiza el proceso
de creación del asiento de cierre del ejercicio contable. Esto significa
que traspasa los saldos de las subcuentas del debe al haber o viceversa
anulando el saldo que tienen en la fecha de fin del ejercicio.

Al iniciar el proceso se elimina cualquier asiento de cierre ya existente dentro del ejercicio.

El asiento que se crea tiene asignado el tipo de operación 'C' que lo identifica
como asiento de cierre.


Métodos principales
===================

La clase puede ser llamada utilizando el método **exec**, informando del ejercicio
y el identificador del diario, para crear el asiento o con el método **delete**, informando
del ejercicio donde se ha de eliminar el asiento.

El parámetro de ejercicio es un objeto del modelo *Ejercicio* con los datos del ejercicio
donde se realiza o se elimina el cierre.


Métodos GET
===========

Estos métodos son llamados para obtener información sobre el cierre.

:getConcept: Retorna el concepto para el asiento y sus líneas. Por defecto 'Cierre del ejercicio' más el nombre del ejercicio.

:getDate: Retorna la fecha establecida como fecha fin del ejercicio.

:getOperation: Retorna el valor *C*.

:getSubAccountsFilter: Retorna la condición where para filtrar las subcuentas entre el grupo **1** y **5**


Métodos SET
===========

Estos métodos se utilizan para establecer datos generales o por defecto.

:setDataLine: Además de asignar los valores por defecto de la línea de asiento, establece los importes del debe y haber.
