.. highlight:: rst
.. title:: Facturascripts Apertura Contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Proceso de apertura contable.
  :keywords: facturascripts, apertura, contabilidad, Apertura Contable, AccountingClosingOpening
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Apertura Contable
  :lang: es


########################
AccountingClosingOpening
########################

Esta clase, que hereda de *AccountingClosingBase*, realiza el proceso
de creación del asiento de apertura del ejercicio. Esto significa
que traspasa los saldos que tenían las subcuentas antes del asiento
del cierre.

Al iniciar el proceso se calcula, y se da de alta si no existe, el nuevo
ejercicio donde se realizará el proceso. También se elimina cualquier asiento
de apertura ya existente dentro del nuevo ejercicio y se crean, copíando del
ejercicio cerrado, las cuentas y subcuentas con saldo.

El asiento que se crea tiene asignado el tipo de operación 'A' que lo identifica
como asiento de apertura.


Métodos principales
===================

La clase puede ser llamada utilizando el método **exec**, informando del ejercicio
y el identificador del diario, para crear el asiento o con el método **delete**, informando
del ejercicio.

El parámetro de ejercicio es un objeto del modelo *Ejercicio* con los datos del ejercicio.

.. warning::
    Para realizar este proceso, el parámetro *Ejercicio* debe contener los datos
    del ejercicio donde se ha realizado el cierre. Esta clase calcula de manera
    automática el ejercicio para la apertura.


Métodos GET
===========

Estos métodos son llamados para obtener información sobre la apertura.

:getConcept: Retorna el concepto para el asiento y sus líneas. Por defecto 'Apertura del ejercicio' más el nombre del nuevo ejercicio.

:getDate: Retorna la fecha establecida como fecha inicio del ejercicio nuevo.

:getOperation: Retorna el valor *A*.

:getOperationFilter: Retorna el valor *C*. Es el tipo de operación de donde saca los saldos de las subcuentas a traspasar al nuevo ejercicio.

:getSQL: Retorna la sentencia SQL para la obtención del balance de subcuentas.
         Este método agrega una nueva columna **id_new** con el identificador de la subcuenta en el nuevo ejercicio.

:getSubAccountsFilter: Retorna la condición where para filtrar las subcuentas entre el grupo **1** y **5**


Métodos SET
===========

Estos métodos se utilizan para establecer datos generales o por defecto.

:setData: Además de asignar los valores por defecto a la cabecera de asiento, establece como ejercicio destino el nuevo ejercicio.

:setDataLine: Además de asignar los valores por defecto de la línea de asiento, establece los importes del debe y haber.
