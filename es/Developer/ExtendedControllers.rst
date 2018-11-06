.. highlight:: rst
.. title:: Facturascripts controladores extendidos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Los controladores extendidos, la novedad de FS 2018. Desarrollo fácil y rápido.
  :keywords: facturascripts, documentacion, desarrollo, controlador, novedad, desarrollo facil, desarrollo rapido


########################
Controladores Extendidos
########################

En *Facturascripts 2018* se ha realizado un esfuerzo por simplificar las tareas *comunes*
a la hora del desarrollo de nuevas personalizaciones. Así se ha creado un conjunto de
clases y protocolos de trabajo que se han denominado **ExtendedControllers**.
Utilizando esta librería es muy sencillo y rápido crear nuevas opciones, manteniendo el estilo y ventajas
incluidas en *Facturascripts* y ahorrarando en código y tiempo de desarrollo.
Además las futuras mejoras que se implementen estarían disponible automáticamente en
el nuevo desarrollo.

Entre muchas características incluidas están:
  - búsquedas, filtrado y navegación entre los datos
  - impresión y exportación de los datos
  - visualización y edición de multiples modelos mediante pestañas
  - diseño de vistas de manera sencilla mediante archivos xml (Ver `Vistas XML <XMLViews>`__)
  - inclusión de elementos visuales como botones, acciones y formularios modales
  - integración con el sistema de traducción


La filosofía de diseño de interfaces de usuario en *Facturascripts 2018* es: **primero listar**,
**depués editar**. Así el usuario primero debe ver un listado con la información sobre la
que puede interactuar (buscar y/o filtrar) y al seleccionar un registro el usuario podrá
editar ese registro de datos.


Uso del controlador
===================

Los controladores extendidos cumplen con lo expuesto en `Controlador <Controllers>`__, y necesitamos
seguir cumpliendo las normas pero variando la clase de la cual heredamos al crear nuestro controlador.
En lugar de extender la clase *Controller*, en función del uso, lo haremos de las clases:

  - **ListController**: Para visualizaciones de uno o varios modelos a modo de consulta.

  - **EditController**: Para la visualización y edición de un único registro de un modelo.

  - **PanelController**: Para la visualización y edición de datos de varios modelos.


Debemos recordar que cada uno de estos controladores ya incluyen los métodos *execPreviousAction* y
*execAfterAction* encargados de controlar y ejecutar las acciones solicitadas por el usuario
mediante la vista. Podemos sobrescribir los métodos para añadir nuevas acciones a controlar.


execPreviousAction
------------------

Se ejecuta justo antes de la carga de datos y tiene la posibilidad de interrumpir la
ejecución del controlador devolviendo *false*. Esto lo hace ideal para tareas especiales
solicitadas desde la vista mediante AJAX. En estos casos no debemos olvidar de desactivar
el proceso de plantillas con *$this->setTemplate(false)*.

Algunas de las tareas que actualmente gestiona:

:autocomplete:  Devuelve un array de datos para realizar el autocompletado de datos.
:save:  Graba los datos enviados al controlador en su modelo.
:delete: Elimina del modelo el registro de datos especificado.


Ejemplo: *Adición de nuevas acciones*

.. code:: php

    protected function execPreviousAction($action)
    {
        switch ($action) {
          case 'clone':
              $data = $this->request->request->all();
              $result = $this->cloneDocument($data);
              if (!empty($result)) {
                  $this->setTemplate(false);
                  $this->response->headers->set('Refresh', '0;' . $result);
                  return false;
              }
              return true;

          case 'lock':
              $data = $this->request->request->all();
              $result = $this->lockDocument($data);
              return true;

          default:
              return parent::execPreviousAction($action);
      }


execAfterAction
---------------

Se ejecuta después de la carga de datos y antes de visualizar los datos al usuario.
Como ya se han leido los datos de los modelos, cualquier cambio que se realice sobre los
datos cargados, no se verán reflejados en su modelo.

Algunas de las tareas que actualmente gestiona:

:insert:  Permite establecer valores por defecto cuando es una alta nueva.
:export:  Envía los datos a la clase que exporta a PDF, CSV o similar.
:megasearch:  Responde a la petición del *Mega Buscador*.


.. code:: php

    protected function execAfterAction($action)
    {
        switch ($action) {
            case 'insert':
                /// Load default values for new record
                $this->views['EditRegularizacionImpuesto']->model->loadNextPeriod();
                break;

            default:
                parent::execAfterAction($action);
        }
    }


Personalización de la vista: Settings
=====================================

Las vistas usadas en los controladores extendidos disponen de la propiedad *settings*
accesible mediante los métodos del controlador **getSettings** y **setSettings** que nos
permiten leer y añadir/modificar los valores, respectivamente, personalizando la vista.
Esta propiedad permite también pasar configuraciones propias de la vista a la plantilla
de manera que estarán disponibles en el código html.twig y en las funciones JavaScripts que
implementemos.

Existen algunos valores ya utilizados por los propios controladores extendidos:

:active: Indica si la vista (pestaña/tab) está activa o apagada (*disabled*).
:icon: Establece el icono para la vista.
:btnNew: Oculta el botón de nuevo.
:btnDelete: Oculta el botón de eliminar.
:btnPrint: Oculta el botón de imprimir.
:megasearch: Indica si la vista está incluida cuando se realiza una búsqueda global.


Establecer Settings
-------------------

La manera de añadir valores de configuración sería, una vez creada la vista, normalmente en el método
*createViews*, llamando al método *setSettings* desde el controlador e indicando la vista, la propiedad y el valor.

.. code:: php

    // Configuración: No responder al megabuscador y no mostrar botón de nuevo
    $this->setSettings('MyView', 'megasearch', false);
    $this->setSettings('MyView', 'btnNew', false);

    // Este es un valor nuevo creado por el desarrollador para algún proposito especial
    $this->setSettings('MyView', 'myconfig', value);


Leer Settings
-------------

La manera de usar o recoger estos valores sería:

.. code:: php

    // Desde PHP
    $active = $this->getSettings('MyView', 'active');
    $myconfig = $this->getSettings('MyView', 'myconfig');


.. code:: html

    <!-- Desde Plantilla TWIG -->
    {% if fsc.getSettings('MyView', 'myconfig') == value %}
        <span>Se cumple la configuración</span>
    {% endif %}

    <!-- Desde JavaScripts -->
    if (Settings['MyView'].myconfig == value) {
        [ ... ]
    }
