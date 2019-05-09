.. highlight:: rst
.. title:: Facturascripts EditController
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Controlador multi panel, nuevo sistema de desarrollo simple
  :keywords: facturascripts, desarrollo, simple, sencillo, paneles, controlador
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: EditController FacturaScripts
  :lang: es


##########################
Controlador EditController
##########################

Es un **controlador universal** para vistas que desean mostrar los datos
completos de un registro de datos de un modelo, en formato “ficha” o
mediante un diseño de columnas agrupadas según el tipo de información.
El uso de este controlador simplifica en gran manera la programación
necesaria para la edición de los datos, así como unificamos la imagen de
la aplicación y plugins creando un entorno uniforme para el usuario lo
que acelera el aprendizaje y adaptación a **Facturascripts**.

Para el uso de este controlador es necesario crear las vistas en formato
XML, tal y como se describe en el documento `XMLViews <XMLViews>`__,
incluido en la documentación de **Facturascripts**.

Cómo usar el controlador
========================

Para utilizar *EditController* debemos crearnos una nueva clase PHP que
herede o extienda de EditController, debiendo crear los métodos:

-  **getModelClassName**: Devuelve el nombre del modelo a editar. El controlador
   buscará automáticamente el archivo XML con nombre *Edit{Nombre del Modelo}* en
   la carpeta XMLView.

-  **getPageData**: Establece los datos generales (título, icono, menú, etc)
   para la vista principal (la primera que añadimos en *createViews*).
   Este método se vió en el apartado :ref:`Controlador <getpagedata>` y
   es obligatorio en todos los controladores.

El controlador *EditController* hereda directamente del controlador *PanelController*
por lo que es posible añadir más vistas/pestañas. Para ello usaremos los métodos **createViews**
y **loadData** tal como se describe en la documentación del `PanelController <PanelController>`__.

Ejemplo con una pestaña adicional

.. code:: php

    protected function createViews()
    {
        parent::createViews();
        $this->addListView('ListProducto', 'Producto', 'products', 'fas fa-cubes');
    }

    protected function loadData($viewName, $view)
    {
        switch ($viewName) {
            case 'ListProducto':
                $codfabricante = $this->getViewModelValue('EditFabricante', 'codfabricante');
                $where = [new DataBaseWhere('codfabricante', $codfabricante)];
                $view->loadData('', $where);
                break;

            default:
                parent::loadData($viewName, $view);
                break;
        }
    }

Establecer Sólo Lectura
=======================
Es posible establecer las vistas *Edit* como sólo lectura desde el controlador. Esto cambia el
template TWig que se usará para renderizar la vista de modo que no se incluirán los botones de
borrado y guardado de datos, además de visualizar los datos sin posibilidad de edición.

Para activar o desactivar esta opción debemos llamar al método **setReadOnly** de la vista.

.. code:: php

    protected function createViews()
    {
        /// Add Views
        parent::createViews();
        $this->addListView('ListEmployeePayRollSalary', 'EmployeePayRollSalary', 'payroll-salary');

        /// Configure views
        $this->views['EditEmployeePayRoll']->setReadOnly(true);
        $this->setSettings('EditEmployeePayRoll', 'btnNew', false);

        /// Set tabs views configuration
        $this->setTabsPosition('bottom');
    }


Personalizar cabecera y pie
===========================
Existen dos métodos que nos permiten personalizar los datos a visualizar en la cabecera y pie de la ficha de datos.

.. code:: php

        public function getPanelHeader()
        {
            return $this->i18n->trans('header-data');
        }

        public function getPanelFooter()
        {
            return $this->i18n->trans('footer-data');
        }

También podemos personalizar la vista mediante la inclusión en el fichero XML del grupo *<rows>*
y crear *<row type=“”>* de las clases **statistics**, para definir una lista de botones estadísticos y
relacionales con otros modelos, y **footer**, para añadir información adicional a visualizar al
usuario justo después de la ficha de datos.

Ejemplos:

.. code:: xml

        <rows>
            <row type="statistics">
                <option icon="fas fa-files-o" label="Alb. Pdtes:" calculateby="nombre_function" onclick="#url"></option>
                <option icon="fas fa-files-o" label="Pdte Cobro:" calculateby="nombre_function" onclick="#url"></option>
            </row>

            <row type="footer">
                <option label="Panel Footer" footer="Panel footer" color="warning">Este es un ejemplo con cabecera y footer</option>
                <option label="Esto es un info" color="info">Este es un ejemplo con cabecera y sin footer</option>
                <option footer="Texto en el footer" color="success">Este es un ejemplo sin cabecera</option>
            </row>
        </rows>
