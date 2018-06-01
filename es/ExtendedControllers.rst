.. highlight:: rst
.. title:: Facturascripts controladores extendidos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Los controladores extendidos, la novedad de FS 2018. Desarrollo fácil y rápido.
  :keywords: facturascripts, documentacion, desarrollo, controlador, novedad, desarrollo facil, desarrollo rapido
  :github_url: https://github.com/ArtexTrading/facturascripts-docs/blob/master/es/ExtendedControllers.rst


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
