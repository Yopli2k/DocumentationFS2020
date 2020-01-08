.. highlight:: rst
.. title:: Facturascripts Cierre contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación Cierre Contable, Regularization, Closing, Opening
  :keywords: facturascripts, cierre contable, regularizacion, cierre, apertura
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Cierre Contable
  :lang: es


###############
Cierre Contable
###############

En *FacturaScripts 2018* se ha potenciado el proceso de cierre contable para facilitar
la personalización de cada uno de los procesos creando métodos **protected** en la mayor
parte de los "pasos" y agrupandolos en clases separadas. Esto permite poder heredar sólo
de los "pasos" que el desarrollador necesita personalizar para el país o cliente concreto
o si lo necesitara sustituir toda una clase por otra que realice distintos procesos.

Cada una de los procesos de creación y borrado de la regularización, cierre y apertura
se han separado en clases independientes que realizan sus tareas propias lo que permite
poder heredar y personalizar por separado cada una de ellos.

La clase principal que realiza las llamadas a cada uno de los procesos es la clase
*ClosingToAcounting*, mientras que las clases *AccountingClosingRegularization*,
*AccountingClosingClosing* y *AccountingClosingOpening* contienen los métodos para
los procesos de regularización, cierre y apertura respectivamente.


.. toctree::
  :caption: Clases
  :maxdepth: 2

  Accounting/ClosingToAcounting
  Accounting/AccountingClosingBase
  Accounting/AccountingClosingRegularization
  Accounting/AccountingClosingClosing
  Accounting/AccountingClosingOpening
