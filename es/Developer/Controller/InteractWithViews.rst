.. highlight:: rst
.. title:: Facturascripts, interacción entre controladores y vistas
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación de ayuda para el desarrollo de Facturascripts 2018
  :keywords: facturascripts, documentacion, desarrollo, plugin, controlador, vista, ejemplos
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Interacturar con Vistas FacturaScripts
  :lang: es


###########################
Interacturar con las Vistas
###########################

Aunque el nuevo sistema de vistas XML pueda parecer estricto, realmente permite al programador
un gran control sobre los objetos de la pantalla a nivel técnico liberándolo de la preocupación
estética y simplificando ese proceso.

Vamos a ver algunos ejemplos de como podemos acceder y variar la configuración desde nuestro controlador
de una columna y de su widget asociado definido en un archivo xml. Para ello vamos a recordar dos conceptos
ya vistos, que los controladores extendidos son contenedores de vistas (:guilabel:`$this->views`) y que
el proceso de carga se realiza según el patrón:

    - **Añadir vista**: Carga la configuración de la vista para el usuario activo.
    - **Cargar datos**: Se realiza la lectura de los datos del modelo de la vista.
    - **"Pintado"** de la vista: Mediante plantilla de twig se compone y visualiza la vista al usuario.

Podemos ver que hay dos procesos donde se han cargado los datos de configuración de la vista
y podemos alterarlos antes de que el usuario reciba la vista. El cúal usar, dependerá de si
necesitamos los datos del modelo para el proceso y de nuestra preferencia.


Seleccionar columnas
====================

Una vez cargada la vista, para poder modificar la configuración de una columna y/o de su widget
primero debemos acceder o seleccionar la columna. Para esto **la vista** tiene dos métodos,
en función del nombre que tiene en el archivo xml o por el nombre de campo de la tabla/modelo,
obteniendo un objeto de la clase :guilabel:`ColumnItem`.

:columnForField: Devuelve la columna que tiene el "fieldname" igual al indicado.
:columnForName: Devuelve la columna que tiene por "name" el indicado.

.. code:: php

    // Establece el tamaño de la columna en 6 y amplia el nivel de seguridad a 50
    $column1 = $this->views['Nombre_de_Vista']->columnForField('codcliente');
    $column1->numColumns = 6;
    $column1->level = 50;

    // Establece una longitud máxima de los datos a 50 caracteres
    $column2 = $this->views['Nombre_de_Vista']->columnForName('customer');
    $column2->widget->maxLenght = 50;


Apagar y encender columnas
==========================

Aunque podemos activar y desactivar columnas mediante la propiedad *readOnly* del widget
de la columna en cuestión, existe un método que nos permite realizarlo de manera más sencilla
y sin necesidad de buscar la columna sino directamente desde la vista. Para ello usaremos
el método *disableColumn* informando del *name* de la columna en el archivo xml y de si
deseamos que esté o no en *disabled*.


.. code:: php

    // Disable mediante Widget (menos recomendado)
    $column = $this->views['Nombre_de_Vista']->columnForField('codcliente');
    $column->widget->readOnly = true;

    // Disable mediante Vista (método directo)
    $this->views['Nombre_de_Vista']->disableColumn('codcliente', true);


Añadir botones de acción
========================
También puede añadir botones de acción en el área asignada para ese efecto (:ref:`Rows Actions <Rows-actions>`)
simplemente usando el método **addButton()**.

.. code:: php

    $newButton = [
    	'action' => 'EditProducto',
    	'icon' => 'fas fa-plus',
    	'label' => 'new',
    	'type' => 'link',
    ];
    $this->addButton('ListProducto', $newButton);


Cargar datos en Input select
============================

Al definir un widget de tipo *select*, es decir una lista de opciones desplegable, definimos
la carga de datos, mediante un modelo, un rango numérico o una lista fija de valores.
Pero en ocasiones la lista de valores está condicionada a distintas circustancias que
hacen imposible establecer los valores de manera fija. Seleccionando la columna y su widget
(debemos tener en cosideración que este proceso es propio del widget *select*) podemos cargar la
lista de valores desde un array de valores o desde un array de registros de datos cargados
mediante la clase *CodeModel*. Estos métodos de carga también nos permite controlar si se
traducirán las etiquetas que se muestran al usuario.

Desde array
-----------

Para cargar los datos de un array llamaremos al método *setValuesFromArray* incluido en el widget,
informando del propio array y si requiere de traducción. El array puede ser de una o dos
dimensiones. En el primer caso se asume que el array **sólo contiene valores** o que el valor y su etiqueta
son lo mismo. Para el segundo caso, un array multidimensional, se asume que cada elemento tiene la
estructura **['title' => 'Texto etiqueta', 'value' => 'valor']**.


.. code:: php

    // Ejemplo Array una dimensión
    $values = ['CIF', 'DNI', 'Passport', 'Other'];
    $column = $this->views['Nombre_de_Vista']->columnForField('id_fiscal');
    $column->widget->setValuesFromArray($values, true);

    // Ejemplo Array multidimensional
    $values = [
        ['title' => 'CIF', 'value' => 1],
        ['title' => 'DNI', 'value' => 2],
        ['title' => 'Passport', 'value' => 3],
        ['title' => 'Other', 'value' => 9]
    ];
    $column = $this->views['Nombre_de_Vista']->columnForField('id_fiscal');
    $column->widget->setValuesFromArray($values, true);


Desde CodeModel
---------------

Para cargar los valores desde un modelo utilizaremos el modelo especial *CodeModel*
que nos permite acceder a los datos de manera directa cuando sólo deseamos un campo código
y su descripción. La manera es llamando al método estático *all* informando los parámetros:

:tableName: Nombre de la tabla o del modelo de donde recoger los datos.
:fieldCode: Nombre del campo que hace la función de código.
:fieldDescription: Nombre del campo que hace la función de descripción.
:addEmpty: (bool) Indica si deseamos un registro en blanco al principio de la lista.
:where: (DataBaseWhere) Filtro opcional que deseamos aplicar a la selección de datos.

.. code:: php

    // Search for client contacts
    $where = [new DataBaseWhere('codcliente', $codcliente)];
    $contacts = CodeModel::all('contactos', 'idcontacto', 'descripcion', true, $where);

    // Load values option to default billing address from client contacts list
    $columnBilling = $this->views['EditCliente']->columnForName('default-billing-address');
    $columnBilling->widget->setValuesFromCodeModel($contacts);


Seleccionar filtros en ListController
=====================================

Para controladores que heredan de ListController y que tienen posibilidad de aplicar filtros,
es posible personalizar o alterar los filtros añadidos a una vista. Para estos casos
debemos seleccionar primero la vista y luego seleccionar el filtro consultando la propiedad
:guilabel:`filters` que contiene un array con cada uno de los filtros definidos (un array de
objetos :guilabel:`BaseFilter`). Para seleccionar el filtro utilizaremos el nombre que indicamos
como *key* al añadirlo a la vista.

.. code:: php

    // Ejemplo de carga manual de valores en filtros de tipo select
    $companyFilter = $this->views['ListEmployee']->filters['company'];
    $companyFilter->options['values'] = $this->codeModel->all('empresas', 'idempresa', 'nombre');

    $departmentsFilter = $this->views['ListEmployee']->filters['company'];
    $departmentsFilter->options['values'] = $this->codeModel->all('departments', 'id', 'name');

    // Ejemplo de captura del valor del filtro
    $companyFilter = $this->views['ListEmployee']->filters['company'];
    if ($companyFilter->value !== '') {
        [ ... custom php code ... ]
    }
