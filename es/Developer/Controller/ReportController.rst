.. highlight:: rst
.. title:: Facturascripts ReportController
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Controlador multi panel para informes
  :keywords: facturascripts, desarrollo, informe, listado, report, simple, sencillo, paneles, controlador
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: ReportController FacturaScripts
  :lang: es


############################
Controlador ReportController
############################

Este controlador es un contenedor de vistas del tipo ReportView, que gestiona automáticamente la
visualización y filtrado de datos, mostrando la información de cada vista en una tabla de filas y
columnas. No permite la edición de los datos pero, adicionalmente, al hacer click sobre una de las
filas se puede mostrar un subinforme, normalmente un detalle o desglose de la fila donde se ha realizado el click.

Para el uso de este controlador es necesario crear las vistas en formato XML, tal y como se
describe en el documento `Vistas XML <XMLViews>`__, incluido en la documentación de **Facturascripts**.

.. important::
    Este controlador hereda del controlador `ListController <ListController>`__ usando su sistema de ordenado y filtros
    con la salvedad de que al editar un valor en el órden o en los filtros no se recalculan los datos.
    Para poder ver el informe se dispone de un botón **Ver Informe** que lanza el proceso de cálculo y visualización.


Cómo usar el controlador
========================

Para utilizar *ReportController* debemos crearnos una nueva clase PHP que herede o extienda de ReportController
y recomendablemente que comience con **Report**, debiendo implementar los siguientes métodos:

-  **createViews**: Encargado de crear y añadir las vistas que deseamos visualizar dentro del ReportController.

-  **getPageData**: Establece los datos generales (título, icono, menú, etc)
   para la vista principal (la primera que añadimos en *createViews*).
   Este método se vió en el apartado :ref:`Controlador <getpagedata>` y
   es obligatorio en todos los controladores.


Añadir y configurar las vistas
==============================

createViews
-----------

Dentro de este método, en nuestra nueva clase, debemos ir creando las distintas vistas que se
visualizarán, y para cada vista indicar la ordenación y filtrados o parámetros del informe.

La manera de añadir una vista es mediante el método **addView** incluido en el propio controlador.
Una vez añadida la vista, debemos configurarla añadiendo la ordenación y los filtros mediante
los métodos **addOrderBy** y **addFilter**. Estos métodos se vieron en *ListController* en los apartados
:ref:`addView <addView>` y :ref:`Adición de filtros <addFilter>`.

.. important::
    Las vistas *ReportView* usadas por este controlador utilizan un modelo del tipo **ModelReport**
    en lugar del modelo de datos *ModelClass*. Para más detalle sobre este tipo de modelo se puede
    consultar en `Modelos para informes <ModelReport>`__.


Plantilla principal y detalle
=============================

Este controlador usa una plantilla de twig para el visionado de los datos principales del informe,
pero es posible indicar una segunda plantilla personalizada para la visualización de un detalle al
hacer click sobre una de las filas del informe.

Para habilitar este efecto se debe indicar el nombre del archivo de la plantilla en la propiedad **templateData** de la vista.
La manera más sencilla es en el método *createViews* tras hacer la llamada al método *addView*.
La plantilla detalle debe realizar el pintado *manualmente* tal como el desarrollador desee visualizar los datos.

.. code:: php

    protected function createViews()
    {
        $this->addView('MyView', 'MyViewReport', 'myview-summary', 'fas fa-object-group');
        $this->views['MyView']->templateData = 'MyView' . 'Data.html.twig';

        // Order by
        $this->addOrderBy('MyView', ['id'], 'employee');
        $this->addOrderBy('MyView', ['name'], 'name');

        // Filters
        $this->addFilterPeriod('MyView', 'date', 'date', 'date');
        $this->addFilterAutocomplete('MyView', 'employee', 'employee', 'id', 'employees', 'CAST(id AS VARCHAR)', 'name');
    }
