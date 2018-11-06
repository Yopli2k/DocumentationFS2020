.. highlight:: rst
.. title:: Facturascripts Extended Controller (controlador avanzado)
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Controlador multi panel, nuevo sistema de desarrollo simple
  :keywords: facturascripts, desarrollo, simple, sencillo, paneles, controlador


##########################
Controlador ListController
##########################

Este controlador es un contenedor de vistas del tipo ListView, que
gestiona automáticamente la visualización y filtrado de datos, mostrando
la información de cada vista en una tabla de filas y columnas. No
permite la edición de los datos pero al hacer click sobre una de las
filas se realiza una llamada automática al controlador de edición del
modelo. Para este evento se utiliza la configuración de la primera
columna que tenga informado el atributo *onclick*.

Para el uso de este controlador es necesario crear las vistas en formato
XML, tal y como se describe en el documento `Vistas XML <XMLViews>`__,
incluido en la documentación de **Facturascripts**.

Cómo usar el controlador
========================

Para utilizar *ListController* debemos crearnos una nueva clase PHP que
herede o extienda de ListController, debiendo implementar los siguientes
métodos:

-  **createViews**: Encargado de crear y añadir las vistas que deseamos
   visualizar dentro del ListController.

-  **getPageData**: Establece los datos generales (título, icono, menú, etc)
   para la vista principal (la primera que añadimos en *createViews*).
   Este método se vió en el apartado :ref:`Controlador <getpagedata>` y
   es obligatorio en todos los controladores.


Añadir y configurar las vistas
==============================

createViews
-----------

Dentro de este método, en nuestra nueva clase, debemos ir creando las
distintas vistas que se visualizarán, y para cada vista debemos indicar
los campos de búsqueda y los campos de ordenación. Opcionalmente
podremos añadir opciones de filtrado para que el usuario pueda
complementar el filtrado de búsqueda existente. Este método tiene una
visibilidad de *protected* de manera que los plugins pueden ir
extendiendo nuestra clase y añadir nuevas vistas, o modificar las
existentes.

La manera de añadir una vista es mediante el método ***addView***
incluido en el propio controlador. Para la correcta llamada al método
debemos informar mediante cadenas de texto: el modelo (Nombre completo),
nombre de la vista XML, el título para la pestaña que visualiza el
controlador y su icono. Si se omite alguno de estos últimos parámetros,
el controlador asignará un texto y/o un icono por defecto.

Una vez añadida la vista, debemos configurarla indicando los campos de
búsqueda y la ordenación mediante los métodos ***addSearchFields*** y
***addOrderBy***.

addSearchFields
---------------

Al añadir los campos de búsqueda debemos indicar el nombre de la vista
al que añadimos los campos y un array con los nombre de los campos.

Ejemplo de creación y adición de campos para búsqueda

.. code:: php

        /* Epigrafes */
        $this->addView('FacturaScripts\Core\Model\Epigrafe', 'ListEpigrafe', 'Epigrafes');
        $this->addSearchFields('ListEpigrafe', ['descripcion', 'codepigrafe', 'codejercicio']);

        /* Clientes */
        $this->addView('FacturaScripts\Core\Model\Cliente', 'ListCliente', 'customers', 'fa-users');
        $this->addSearchFields('ListCliente', ['nombre', 'razonsocial', 'codcliente', 'email']);

        /* Grupos */
        $this->addView('FacturaScripts\Core\Model\GrupoClientes', 'ListGrupoClientes', 'groups', 'fa-folder-open');
        $this->addSearchFields('ListGrupoClientes', ['nombre', 'codgrupo']);

addOrderBy
----------

Podemos añadir todos los campos de ordenación, no confundir con los campos de búsqueda, realizando
distintas llamadas al método *addOrderBy* e indicando el nombre de la vista a la que añadimos
la ordenación, una o varias expresiones de ordenación (cualquier expresión aceptada por la cláusula
ORDER BY de SQL), texto a visualizar al usuario y el indicativo de orden
por defecto.

Consideraciones:

- Si se indica una única expresión de ordenación usaremos la expresión entre comillas a modo de cadena de texto.

- Si se indican múltiples expresiones de ordenación usaremos un array de cadenas de texto.

- Si no se indica texto a visualizar, se empleará el valor informado en la expresión de
  ordenación (aplicando el sistema de traducciones). Se recomienda informar este texto
  para evitar traducciones erróneas.

- Si no se indica valor de ordenación por defecto, se entiende que no hay una ordenación por defecto
  y se aplicará el primer orden añadido.

- Al añadir una ordenación **siempre** se añaden dos opciones de ordenación, una ascendente y otra descendente.

- Para establecer una ordenación por defecto, al añadir la ordenación podemos indicar como valores 1 para la ascendente y 2 para la descendente.


Ejemplo de adición de ordenación (siguiendo el ejemplo anterior) con ordenación por código descendente

.. code:: php

        /* Epigrafes */
        $this->addOrderBy('ListEpigrafe', 'descripcion', 'description');
        $this->addOrderBy('ListEpigrafe', 'CONCAT(codepigrafe, codejercicio)', 'code', 2);
        $this->addOrderBy('ListEpigrafe', 'codejercicio');

        /* Clientes */
        $this->addOrderBy('ListCliente', 'codcliente', 'code');
        $this->addOrderBy('ListCliente', 'nombre', 'name', 1);
        $this->addOrderBy('ListCliente', 'fecha', 'date');
        $this->addOrderBy('ListCliente', ['codgrupo', 'codcliente'], 'group');

        /* Grupos */
        $this->addOrderBy('ListGrupoClientes', 'codgrupo', 'code');
        $this->addOrderBy('ListGrupoClientes', 'nombre', 'name', 1);

Adición de filtros
==================

El controlador *ListController* integra un sistema de filtrado de datos
que permite personalizar de manera sencilla las opciones de filtrado que
se presentan al usuario. Cada tipo de filtro requiere de una
parametrización propia para su funcionamiento como el nombre de la vista
a la que lo añadimos, y entre los tipos de filtros disponibles están:

:addFilterAutocomplete:
    Filtro tipo texto donde al escribir el usuario se realiza una consulta al servidor
    recibiendo una lista de datos que contienen el texto introducido por el usuario.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key : Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.
    - table: Nombre de la tabla o modelo donde se realizará la búsqueda de datos.
    - fieldcode: Nombre del campo PK de la tabla indicada en *table*. Opcional.
    - fieldtitle: Nombre del campo con la descripción. Opcional.
    - where: Filtro `DataBaseWhere <DataBaseWhere>`__ que se aplicará adicionalmente a la tabla indicada.


:addFilterCheckbox:
    Filtro tipo checkbox o de selección booleana.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.
    - operation: Operador lógico que se aplicará a la condición de filtrado. Por defecto '='.
    - matchValue: Permite especificar el valor a comprobar. Por defecto un valor verdadero.
    - default: Filtro `DataBaseWhere <DataBaseWhere>`__ que se aplicará cuando el filtro no esté seleccionado.


:addFilterDatePicker:
    Filtro de tipo fecha que permite seleccionar de un calendario que se despliega al seleccionarse el filtro.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.
    - operation: Operador lógico que se aplicará a la condición de filtrado. Por defecto '>='.


:addFilterNumber:
    Filtro de tipo numérico y/o importes.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.
    - operation: Operador lógico que se aplicará a la condición de filtrado. Por defecto '>='.


:addFilterPeriod:
    Filtro para seleccionar periodo de fechas mediante la selección de un periodo de una lista
    o por la introdución de la fecha de inicio y fin. Este filtro al ser añadido añade un filtro
    de tipo *Select* y dos filtros de tipo *DatePicker* ocupando 3 columnas. Esto es importante
    a la hora de su posicionamiento en la vista si deseamos que no queden cortadas las columnas
    en distintas lineas.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.


:addFilterSelect:
    Filtro tipo selección de una lista de valores.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - label: Etiqueta informativa para el usuario. Se traduce automáticamente.
    - field: Nombre del campo donde se aplica el filtro. Si no se indica se usa el valor de key.
    - values: Lista de valores a visualizar. Debe ser un array con la estructura:

    .. code:: php

        [ 'key1' => 'value1', 'key2' => 'value2', 'keyN' => 'valueN']



:addFilterSelectWhere:
    Filtro tipo selección de una lista de valores.

    - viewName: Nombre de la vista donde se añade el filtro.
    - key: Es el nombre interno del filtro. Debe ser único para la vista.
    - values: Es un array con las opciones y condiciones que se aplicarán. Debe ser un array con la estructura:

    .. code:: php

        [
          ['label' => 'only-active', 'where' => [ new DataBaseWhere('suspended', 'FALSE') ]],
          ['label' => 'only-suspended', 'where' => [ new DataBaseWhere('suspended', 'TRUE') ]],
          ['label' => 'all', 'where' => []]
        ]


Ejemplos de filtros
-------------------

.. code:: php

        $this->addFilterSelect('ListEpigrafe', 'codepigrafe', 'co_epigrafes', '', 'descripcion');
        $this->addFilterCheckbox('ListCliente', 'debaja', 'De baja');
        $this->addFilterDatePicker(ListArticulo, 'fecha', 'Fec. Alta');
