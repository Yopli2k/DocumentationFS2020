.. highlight:: rst
.. title:: Facturascripts configurar: Régimen del Impuesto
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Configurar régimen del Impueto en FacturaScripts 2018.
  :keywords: facturascripts, configurar, impuestos, IVA
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Configurar Régimen Impuesto FacturaScripts 2018
  :lang: es

####################
Régimen del Impuesto
####################

Facturascripts implementa un sistema de hasta tres niveles distintos de aplicación de impuestos.
Estos niveles los denominamos regímenes. Estos regímenes se deben establecer:

    - en las empresas: Editando la ficha, apartado *Avanzado*
    - en los clientes: Editando la ficha, apartado *Términos comerciales*
    - en los proveedores: Editando la ficha, apartado *Términos comerciales*


Régimen General
===============

Este régimen resulta aplicable cuando no es necesario uno de los regímenes especiales. Al seleccionarlo
se aplicará el tipo impositivo indicado, es decir el tipo de impuesto seleccionado y de este el porcentaje.

Hay que resaltar que en el cálculo del pocentaje a aplicar se tiene en cuenta la configuración de *Zonas de Impuestos* introducida.

.. note::
    En la actualidad y de forma general *(existen zonas con distintos porcentajes)*,
    los porcentajes de IVA aplicables en España son:
        - Super Reducido: 4% - para productos de primera necesidad
        - Reducido: 10% - para productos y servicios especiales
        - General: 21% - para productos y servicios no incluidos en los apartados anteriores


Recargo de Equivalencia
=======================

Este es un régimen especial al que se acogen exclusivamente los comerciantes, que no son sociedad, y venden al cliente final.
Los que utilizan este régimen están obligados a pagar un porcentaje de impuesto adicional al impuesto del producto y/o servicio
en el momento de la compra a cambio de realizar la autoliquidación del impuesto.

Al seleccionar este régimen se suma al porcentaje del impuesto seleccionado el porcentaje indicado en el campo *recargo de equivalencia*.

.. note::
    En la actualidad y de forma general *(existen zonas con distintos porcentajes)*,
    los porcentajes de recargo de equivalencia aplicables en España son:
        - Super Reducido: 0,5% - para productos de primera necesidad
        - Reducido: 1,4% - para productos y servicios especiales
        - General: 5,2% - para productos y servicios no incluidos en los apartados anteriores


Régimen Exento
==============

Este régimen se aplica a algunas organizaciones como fundaciones, ongs, academias, y en algunas
operaciones de compra y venta como las compras intracomunitarias. Al aplicarlo estamos indicando
que la operación no lleva ningún cargo de impuesto por lo que no se aplica ningún porcentaje.
