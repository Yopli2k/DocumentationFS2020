.. highlight:: rst
.. title:: Contabilización del cierre
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación técnica de la Contabilización del Cierre de ejercicio
  :keywords: facturascripts, documentacion, ejercicio, cierre, cierre contable, asientos
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: ClosingToAcounting FacturaScripts
  :lang: es


##################
ClosingToAcounting
##################

Esta clase realiza la generación de asientos contables de la regularización, cierre y
apertura de ejercicio de manera automatizada. Todos sus métodos son de nivel **public**
o **protected** lo que permite la personalización en caso necesario por ejemplo para
distintos países simplemente heredando.

Los métodos públicos son la entrada a los dos procesos principales (creación y borrado)
y reciben como parámetros el código que identifica el ejercicio que se desea cerrar y del
cual se calculará (se dará de alta de manera automática si no existe) el ejercicio nuevo a abrir, y un
array con distintos valores denominado **$data** que permiten configurar el proceso. Este parámetro
permite de manera sencilla que procesos heredados puedan añadir nuevos valores sin modificar las
llamadas ya existentes a los métodos.


Método exec
===========
Es el método principal para la generación de los asientos. Actualmente el parámetro **$data** puede
recibir dos valores *journalClosing* y *jornalOpening* con los identificadores de los diarios contables
donde se generarán los asientos.  

El conjunto de procesos, regularización, cierre y apertura, se realizan mediante llamadas a métodos protected
con el nombre del proceso precedido del sufijo **exec**.

Al finalizar los subprocesos, si estos indican que todo ha resultado correcto, se actualiza el estado
del ejercicio a **cerrado**.

La ejecución de cada uno de los procesos sigue el siguiente patrón:

1. Se obtiene el balance de las subcuentas con saldo para cada canal utilizado. El conjunto de cuentas depende de si es regularización, cierre o apertura.
2. Por cada canal, se crea un asiento contable donde se graban las subcuentas con saldo para ese canal.
3. Se crea una línea de "cierre" de todos los saldos del canal, en caso de que sea necesaria.
4. Se actualiza el importe final del asiento contable.

.. note::
    Como se ha comentado anteriormente, existen métodos protected para cada uno de los pasos, y es recomendable, para un mayor detalle
    consultar las clases de reguralización, cierre y/o apertura.

    Documentación de la regularización `AccountingClosingRegularization <AccountingClosingRegularization>`__.

    Documentación del cierre contable `AccountingClosingClosing <AccountingClosingClosing>`__.

    Documentación de la apertura `AccountingClosingOpening <AccountingClosingOpening>`__.


execRegularization
------------------

Este método se encarga de crear la clase encargada de generar la regularización del ejercicio y ejecutar su método **exec**
informando del ejercicio y del identificador del diario.


execClosing
-----------

Este método se encarga de crear la clase encargada de realizar el cierre del ejercicio y ejecutar su método **exec**
informando del ejercicio y del identificador del diario.


execOpening
-----------

Este método se encarga de crear la clase encargada de realizar la apertura del nuevo ejercicio y ejecutar su método **exec**
informando del ejercicio y del identificador del diario.


Método delete
=============
Es el proceso para la eliminación de los asientos y reapertura del ejercicio.
El parámetro **$data** puede recibir *deleteClosing* y *deleteOpening*, dos valores booleanos,
que indican si se desea eliminar el asiento contable de cierre y de apertura respectivamente.
Esto permite poder eliminar el asiento contable de cierre sin eliminar la apertura en el nuevo
ejercicio para poder tener de manera temporal informes o balances del nuevo año con saldo inicial
cuando todavía no deseamos cerrar el ejercicio.


deleteRegularization
--------------------

Este método se encarga de crear la clase encargada de controlar la regularizacion de ejercicio y ejecutar su método **delete**
informando del ejercicio de donde eliminar el asiento.


deleteClosing
-------------

Este método se encarga de crear la clase encargada de controlar el cierre de ejercicio y ejecutar su método **delete**
informando del ejercicio de donde eliminar el asiento.


deleteOpening
-------------

Este método se encarga de crear la clase encargada de controlar la apertura de ejercicio y ejecutar su método **delete**
informando del ejercicio de donde eliminar el asiento.
