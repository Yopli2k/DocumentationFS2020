.. highlight:: rst
.. title:: Facturascripts PanelController
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Controlador multi panel, nuevo sistema de desarrollo simple
  :keywords: facturascripts, desarrollo, simple, sencillo, paneles, controlador
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: PanelController FacturaScripts
  :lang: es


###########################
Controlador PanelController
###########################

Este controlador, al igual que el controlador `ListController <ListController>`__ es un
**controlador universal** para multiples vistas/pestañas aunque en este caso se
permite el uso de distintos tipos de vistas:

- **ListView**: muestra la información a modo de listado.

- **EditView**: visualiza una ficha con la información para su edición.

- **EditListView**: muestra una lista de fichas para la edición múltiple.

- **GridView**: visualiza la información a modo de hoja de cálculo.

- **HTMLView**: muestra una plantilla html de libre diseño.

El controlador divide la pantalla en dos zonas, por defecto, una a la izquierda (zona
de navegación) y otra la derecha donde se visualizan las vistas con los
datos. La zona de navegación puede configurarse para ocupar el lado izquierdo, arriba o abajo.

Para el uso de este controlador es necesario crear las vistas en formato
XML, tal y como se describe en el documento
`XMLViews <XMLViews>`__, incluido en la documentación de **Facturascripts**.

Cómo usar el controlador
========================

Para utilizar *PanelController* debemos crearnos una nueva clase PHP que
herede o extienda de la clase PanelController, debiendo implementar los
siguientes métodos:

-  **createViews**: Encargado de crear y añadir las vistas que deseamos
   visualizar dentro del PanelController.

-  **loadData**: Encargado de cargar los datos para cada una de las
   vistas.

-  **getPageData**: Establece los datos generales (título, icono, menú, etc)
   para la vista principal (la primera que añadimos en *createViews*).
   Este método se vió en el apartado :ref:`Controlador <getpagedata>` y
   es obligatorio en todos los controladores.


Añadir y configurar las vistas
==============================

createViews
-----------

Dentro de este método, en nuestra nueva clase, debemos ir creando las
distintas vistas/pestañas que se visualizarán, debiendo usar distintos métodos
según el tipo de vista que estamos añadiendo. Debemos indicar mediante
cadenas de texto, al añadir una vista, el modelo (Nombre completo) y el
nombre de la vista XML, y opcionalmente el título y el icono para el
grupo de navegación.

-  **addEditView**: Añade una vista para editar datos de un único
   registro de un modelo.

-  **addEditListView**: Añade una vista para editar multiples registros
   de un modelo.

-  **addListView**: Añade una vista para visualizar en modo lista
   multiples registros de un modelo.

-  **addHtmlView**: Añade una vista de libre diseño HTML por parte del desarrollador.

-  **addGridView**: Añade una vista que permite editar los datos en un grid
   de datos de filas y columnas al estilo de una hoja de cálculo.

.. code:: php

        $this->addEditView('EditCliente', 'Cliente', 'Cliente');
        $this->addEditListView('EditDireccionCliente', 'DireccionCliente', 'Direcciones', 'fas fa-road');
        $this->addListView('ListCliente', 'Cliente', 'Mismo Grupo', 'fas fa-person');

Existe la posibilidad de añadir varias vistas/pestañas para un mismo modelo y usando la misma vista XML.
Para ello, al añadir la vista debemos un índice numérico empezando por 1 y separando el nombre de la vista del índice
con un guión *('-')*.

Ejemplo.

.. code:: php

        $this->addListView('ListPartidaImpuesto-1', 'PartidaImpuesto', 'purchases', 'fas fa-sign-in-alt');
        $this->addListView('ListPartidaImpuesto-2', 'PartidaImpuesto', 'sales', 'fas fa-sign-out-alt');


Este método tiene una visibilidad de *protected* de manera que los plugins pueden ir extendiendo
nuestra clase y añadir nuevas vistas, o modificar las existentes.


Sólo lectura
------------

Es posible establecer la vista que hemos añadido como sólo lectura. Esto cambia el template TWig que
se usará para renderizar la vista de modo que no se incluirán los botones de borrado y guardado de datos,
además de visualizar los datos sin posibilidad de edición.

Para activar o desactivar esta opción debemos llamar al método **setReadOnly()** de la vista.

Ejemplo.

.. code:: php

    protected function createViews()
    {
      $this->addEditView('EditInfoProject', 'WebProject', 'project', 'fas fa-info');
      $this->views['EditInfoProject']->setReadOnly(true);
    }


loadData
--------

Este método es llamado por cada una de las vistas para que podamos
cargar los datos específicos de la misma. En la llamada se nos informa
del identificador de la vista y el propio objeto view, pudiendo acceder
a todas las propiedades del mismo. La carga de datos puede variar según
el tipo de vista, por lo que es responsabilidad del programador realizar
la carga de datos correctamente. Aunque esto pueda suponer una
dificultad añadida, también nos permite un mayor control sobre los datos
que a leer del modelo.

Tenga en cuenta que se usa **code** como parámetro para indicar el valor de la clave primaria
del registro del modelo de la vista principal (la primera vista añadida). Para el
resto de vistas se recomienda usar el método **getViewModelValue** para obtener el valor principal
porque en el caso de que se acabe de crear el registro principal, el parámetro code todavía no estará
disponible para su uso.


Ejemplo de carga de datos para distintos tipos de vistas.

.. code:: php

        switch ($keyView) {
            case 'EditCliente':
                $value = $this->request->get('code');   // Recoge el código a leer
                $view->loadData($value);                // Carga los datos del modelo para el codigo
                break;

            case 'EditDireccionCliente':
                // creamos un filtro where para recoger los registros pertenecientes al código informado
                $where = [new DataBase\DataBaseWhere('codcliente', $this->getViewModelValue('codcliente'))];
                $view->loadData($where);
                break;

            case 'ListCliente':
                // cargamos datos sólo si existe un grupo informado
                $codgroup = $this->getViewModelValue('codgrupo');

                if (!empty($codgroup)) {
                    $where = [new DataBase\DataBaseWhere('codgrupo', $codgroup)];
                    $view->loadData($where);
                }
                break;
        }


setTabsPosition
---------------

Este método permite poner las pestaña a la izquierda (left), abajo
(bottom) o arriba (top). Por defecto están colocadas a la izquierda.

Las pestañas cuando están colocadas a la izquierda, se mostrara la información
de la pestaña seleccionada. En estos caso no es necesario especificar el método.

Cuando están colocadas abajo, se muestra ventana principal (primera vista que se añade)
y debajo de esta mostrara la información de la pestaña seleccionada. Si sólo hay una vista/pestaña
(a demás de la vista principal) se muestra directamente la vista sin el diseño de pestañas.

Ejemplo.

.. code:: php

    $this->addEditView('FacturaScripts\Core\Model\Asiento', 'EditAsiento', 'accounting-entries', 'fa-balance-scale');
    $this->addListView('FacturaScripts\Core\Model\Partida', 'ListPartida', 'accounting-items', 'fa-book');
    $this->setTabsPosition('bottom');

Cuando están colocadas arriba, se mostrará la información de la pestaña seleccionada.

Ejemplo.

.. code:: php

    $this->addEditView('FacturaScripts\Core\Model\Asiento', 'EditAsiento', 'accounting-entries', 'fa-balance-scale');
    $this->addListView('FacturaScripts\Core\Model\Partida', 'ListPartida', 'accounting-items', 'fa-book');
    $this->setTabsPosition('top');
