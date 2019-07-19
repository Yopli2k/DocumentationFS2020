.. highlight:: rst
.. title:: Facturascripts configurar: Secuencias de Documentos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Configurar las secuencias de documentos en FacturaScripts 2018.
  :keywords: facturascripts, configurar, secuencia, documento, numero de secuencia
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Configurar Secuencias de Documentos FacturaScripts 2018
  :lang: es


########################
Secuencias de Documentos
########################

Con las secuencias podemos definir tanto en el número con el que deben iniciar los documentos
(presupuestos, pedidos, albaranes y facturas) como el código a utilizar.

Para consultar o modificar la lista de secuencias de documentos debemos ir a la opción del
menú (:guilabel:`Administrador->Secuencias de documentos`).

:Tipo de documento: Indica si el documento es un albarán de cliente, albarán de proveedor, factura de cliente, etc.
:Empresa: Indica la empresa en donde se aplica.
:Ejercicio: Indica el ejercicio al que se aplica. Si no se selecciona ninguno, se aplica para todos (excepto para aquellos ejercicios que si tengan una secuencia asignada).
:Serie: Indica la serie a la que se aplica.
:Número: Muestra el próximo número a utilizar.
:Longitud: Indica la longitud máxima deseada. Se añadiran los ceros necesarios hasta que la longitud del número sea la indicada.
:Patrón: Fórmula base a utilizar para el cálculo del código del documento. Este patrón admite variables que son sustituidas por su valor.

    +---------------+---------------------------------------------------------------+
    | *Variables*   | *Descripción*                                                 |
    +---------------+---------------------------------------------------------------+
    | **{EJE}**     | El ejercicio del documento. p.e: 2019                         |
    +---------------+---------------------------------------------------------------+
    | **{SERIE}**   | La serie del documento. p.e: A                                |
    +---------------+---------------------------------------------------------------+
    | **{0SERIE}**  | La serie del documento, con ceros hasta 2 caracteres. p.e: 0A |
    +---------------+---------------------------------------------------------------+
    | **{NUM}**     | Número del documento. p.e: 47                                 |
    +---------------+---------------------------------------------------------------+
    | **{0NUM}**    | Número del documento, pero relleno con ceros. p.e: 000047     |
    +---------------+---------------------------------------------------------------+

:Título: Título opcional para el documento. Por ejemplo: *Factura Proforma*.


Ejemplos: *Patrones de ejemplo*

.. code::

    FAC + el ejercicio + la serie + el número del documento:
    FAC{EJE}{SERIE}{NUM} -> FAC2019A47

    Serie + el número relleno con ceros:
    {SERIE}{0NUM} -> Ejemplo: A000047
