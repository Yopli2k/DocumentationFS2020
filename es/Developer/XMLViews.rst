.. title:: XML Views
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de vistas mediante XML
  :keywords: facturascripts, documentacion, diseño, vista, xml, desarrollo


##########
Vistas XML
##########

.. important::

    El uso de este tipo de vista es exclusivo de los controladores extendidos.


Tipos y estructura
==================

Las vistas, en *Facturascripts 2018* están clasificadas según su representación
en pantalla tanto en la forma de visualizar como en número de registros de datos.
Así existen distintos tipos de vistas para listar y editar la información, cada una
de ellas personalizable y con elementos propios del tipo de vista.

-  **ListView** : Vistas que muestran una lista de datos en formato de filas y columnas
   pudiendo navegar, buscar y/o filtrar por los datos pero donde los datos son de
   sólo lectura, es decir no se permite su edición.

-  **EditView** : Vistas que muestran un formulario de edición de un único registro de
   datos, pudiendo estar estos datos agrupados en filas y/o columnas según el diseño
   de pantalla establecido por el desarrollador.

-  **EditListView** : Vista resultante de la "unión" de los tipos anteriores. Es decir,
   una lista de registros visualizados en filas y columnas pero donde cada uno de las
   filas es un formulario de edición que nos permite editar los datos de un registro.

-  **GridView** : Vista que depende de una vista padre de tipo **Edit** y en la que la representación
   y manipulación de los datos viene dada por un grid de filas y columnas al estilo de una hoja de cálculo.
   Este tipo de vista requiere de un archivo JavaScript donde se controlan distintos eventos como la
   creación del data grid y eventos de visualización y edición de datos.
   Para más información ver `GridViews <GridViews>`__.

El nombrado de las vistas, cuando las creamos, sigue la siguiente regla: *List* o *Edit* seguido
del *nombre del modelo*. Esto se cumple aún cuando la vista sea del tipo *EditList* o *GridView* en cuyo caso
se nombrará como si fuera del tipo *Edit*.

Para crear las vistas usaremos un archivo con estructura **XML** y, como se ha indicado
anteriormente, con el nombre del tipo de vista y el modelo, donde estableceremos la
composición visual de los campos, las acciones y opciones visuales de la vista.

El elemento raíz del archivo XML será **<view>** donde se debe incluir la etiqueta *<columns>*
y de manera opcional se pueden incluir las etiquetas *<rows>* y *<modals>*. Cada una de las etiquetas
funcionan a modo de grupo, es decir simplemente las declaramos y dentro incluiremos las opciones
visuales a "pintar" en la pantalla. Cada grupo desempeña una funcionalidad distinta:

-  **columns** : (obligatorio) Se usa para definir la lista de campos que se
   visualizan en la vista mediante la definición de etiquetas *<column>* (en singular) donde
   se define el widget que se pintará en la pantalla. En las vistas de tipo *Edit*, se pueden agrupar
   varias etiquetas *<column>* dentro de una etiqueta *<group>* permitiendo crear diseños
   personalizados o mejor estructurados. Más información sobre las `columnas <XMLColumns>`__.

-  **rows** : (opcional) Esta etiqueta nos permite definir condiciones especiales para
   la aplicación de colores a las filas, añadir distintos tipos botones (estadísticos,
   acción y JavaScript) a las vistas y la inserción de paneles (cards de bootstrap)
   para mostrar información personalizada. Más información sobre los `rows <XMLRows>`__.

-  **modals** : (opcional) Define formularios modales que son visualizados
   mediante la interacción del usuario con un botón definido en la vista. La definición
   de los campos a incluir en los formularios es similar al usado para declarar los
   campos en la etiqueta *<columns>*. Más información sobre los `modals <XMLModals>`__.


Otros conceptos
===============

Múltiples usos de la vista
--------------------------
En ocasiones podemos necesitar mostrar la misma vista o archivo xml pero con un filtrado
de datos distinto.

Ejemplo:
    - Lista de partidas de asientos de tipo compras
    - Lista de partidas de asientos de tipo ventas


Para estos casos podemos incluir la vista xml añadiendo el separador '**-**' seguido de un
**identificador único**.

.. code:: php

    $this->addListView('ListPartidaImpuesto-1', 'PartidaImpuesto', 'purchases', 'fas fa-sign-in-alt');
    $this->addListView('ListPartidaImpuesto-2', 'PartidaImpuesto', 'sales', 'fas fa-sign-out-alt');


Múltiples usos del modelo
--------------------------
También nos puede interesar, sobretodo si el modelo tiene muchos campos, separar los
campos del modelo en varias vistas xml. En este caso debemos tener en cuenta que la
vista principal debe tener todos los campos obligatorios o requeridos ya que las vistas
secundarias no están disponibles cuando se está dando de alta un nuevo registro en el
modelo.

.. code:: php

    // Los datos de baja y notas/observaciones del empleado se ponen en otra vista
    $this->addEditView('EditEmployee', 'Employee', 'employee', 'fas fa-id-card');
    $this->addEditView('EditEmployeeNote', 'Employee', 'notes', 'fas fa-sticky-note');
