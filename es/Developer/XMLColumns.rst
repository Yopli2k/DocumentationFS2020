.. title:: XML Columns
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas. Configuración de columnas
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de columnas en vistas XML.
  :keywords: facturascripts, documentacion, diseño, columna, widget, vista, xml, desarrollo


####################
Vistas XML: Columnas
####################

Etiqueta columns
================

Permite definir mediante la etiqueta *<column>* cada uno de los campos que se visualizarán
en la vista pudiendo, en las vistas *Edit*, agrupar las columnas mediante la etiqueta *<group>*.
Las columnas, se complementan con la etiqueta *<widget>*, que sirve para personalizar
el tipo de objeto que se usa en la visualización/edición del dato, o con la etiqueta *<button>*
para indicar un bottón.

Tanto las etiquetas *<group>*, *<column>* como *<widget>* disponen de un conjunto de atributos
que permiten la personalización y que varían según el contexto en que se ejecutan, es decir si
es una vista *List* o una vista *Edit*. Es posible indicar el número de columnas que ocupará
*<column>* y/o el grupo *<group>* dentro de la rejilla bootstrap (por defecto el máximo disponible).

Ejemplo vista para ListController:

.. code:: xml

      <columns>
          <column name="code" display="left" order="100">
              <widget type="text" fieldname="codigo" onclick="EditMyModel" />
          </column>
          <column name="description" display="left" order="105">
              <widget type="text" fieldname="descripcion" />
          </column>
          <column name="state" display="center" order="110">
              <widget type="text" fieldname="estado">
                  <option color="red" font-weight="bold">ABIERTO</option>
                  <option color="blue">CERRADO</option>
              </widget>
          </column>
      </columns>

      <rows>
          <row type="status" fieldname="estado">
              <option color="info">Pendiente</option>
              <option color="warning">Parcial</option>
          </row>
      </rows>

Ejemplo de vista para EditController:

.. code:: xml

      <columns>
          <group name="data" numcolumns="8" title="Identificación internacional" icon="fa-globe">
              <column name="code" display="left" numcolumns="4" order="100">
                  <widget type="text" fieldname="codigo" onclick="EditMyModel" />
              </column>
              <column name="description" display="left" numcolumns="8" order="105">
                  <widget type="text" fieldname="descripcion" />
              </column>
          </group>
          <group name="state" numcolumns="4">
              <column name="state" display="center" order="100">
                  <widget type="text" fieldname="estado">
                      <option color="red" font-weight="bold">ABIERTO</option>
                      <option color="blue">CERRADO</option>
                  </widget>
              </column>
          </group>
      </columns>


column
------

Entendemos que es cada uno de los campos del modelo y botones que componen la
vista y con los que el usuario puede interactuar. La etiqueta *column* requiere contener
una de las etiquetas *<widget>* o *<button>* para su funcionamiento y se personaliza
mediante las siguientes propiedades:

:name: Identificador interno de la columna. **Es obligatorio su uso**. Como norma se recomienda
    el uso de identificadores en minúsculas y en inglés.

:level: Sólo los usuarios con un nivel igual o superior verán la columna. Por defecto 0.

:id: Identificador html que se aplica al objeto. Recordar que no se pueden duplicar dentro del
    código HTML por lo que es responsabilidad del desarrollador asegurarse de establecer un
    identificador único. Se recomienda no usar este atributo excepto por necesidad para
    procesos posteriores con el objeto como desde JavaScript. **Opcional**

:title: Etiqueta descriptiva del campo, en caso de no informarse se asume el valor de name.

:titleurl: URL destino si el usuario hace click sobre el título de la columna.

:description: Descripción larga del campo que ayuda la comprensión al usuario. Se traduce automáticamente.
   En las vistas List se muestra como un hint sobre el título de la columna.
   En las vistas Edit se muestra como un label inferior a la zona de edición del campo.

:display: Indica si se visualiza o no el campo y su alineación. Si no se informa, toma como valor *left*.
    Valores: *[left|center|right|none]*

:order: Posición que ocupa la columna. Sirve para indicar el orden en que se visualizan.
    Si no se informa toma el valor *100* Cuando no se informa una ordenación específica,
    se ordena por la posición secuencial en el archivo XML, siempre dentro de su grupo.

:numcolumns: Fuerza el tamaño de la columna al valor indicado, usando el sistema de grid
    de Bootstrap siendo mínimo 1 y máximo 12. Si no se informa toma como valor *0*
    aplicando el sistema de tamaño automático de Bootstrap.


.. important::

    El atributo **id** debe tener un valor único para todo el html de la página.
    Es responsabilidad del desarrollador cumplir con las normas de HTML5 en referencia
    a los identificadores únicos.


widget
------

Complemento visual que se utiliza para la visualización y/o edición del campo/columna.
Cada uno de los widgets disponibles es una clase que se autogestiona, es decir que controla
la lectura del valor y su pintado en pantalla según el tipo de vista que la ejecuta.
Cada widget dispone de una lista de atributos para su inicialización y personalización,
y aunque en su mayoría son comunes cuanto más específicas/complejas son las tareas a realizar
por el widget, este puede necesitar atributos exclusivos de esa clase de widget.

Para las vistas de tipo *List*, se puede aplicar la clusula html *style* a aplicar a la columna
mediante la declaración de una lista de etiquetas **<option>** (dentro de la etiqueta *<widget>*),
donde cada atributo de la etiqueta *<option>* se corresponde con su equivalente CSS que se desea
aplicar y el valor de la etiqueta es el valor cuando se aplicará el formato.
Para decidir si se aplica el formato o no se aplicará los siguientes criterios al valor
introducido en la etiqueta **<option>**:

-  Si el valor empieza por ``>``: Se aplicará si el valor del campo del modelo es mayor que el valor indicado después del operador.

-  Si el valor empieza por ``<``: Se aplicará si el valor del campo del modelo es menor que el valor indicado después del operador.

-  Si el valor empieza por ``!``: Se aplicara si el valor del campo del modelo es diferente que el valor indicado después del operador.

-  En cualquier otro caso se realizará una comprobación de igualdad, es decir que el valor del campo del modelo es igual al valor indicado.


Ejemplos:

*Pintar de color rojo cuando el valor del campo* ``pendiente`` *es cero*

.. code:: xml

      <widget type="checkbox" fieldname="pendiente">
          <option color="red">0</option>
      </widget>

*Pintar de color rojo y negrita cuando el valor del campo* ``estado`` *es* ``ABIERTO``
*Pintar de color azul cuando el valor del campo* ``estado`` *es* ``CERRADO``

.. code:: xml

      <widget type="text" fieldname="estado">
          <option color="red" font-weight="bold">ABIERTO</option>
          <option color="blue">CERRADO</option>
      </widget>

*Pintar de color rojo cuando el valor del campo* ``cantidad`` *es menor de 0*

.. code:: xml

      <widget type="number" fieldname="cantidad">
          <option color="red">&lt;0</option>
      </widget>

*Pintar de color rojo cuando el valor del campo* ``importe`` *es mayor de treinta mil*

.. code:: xml

      <widget type="money" fieldname="importe">
          <option color="red">&gt;30000</option>
      </widget>


Tipos de Widgets
^^^^^^^^^^^^^^^^

Para indicar el tipo o clase de objeto visual utilizamos la etiqueta (obligatoria) **type**
con uno de los siguientes valores:

:text, textarea: Campos de texto o áreas de texto multilínea.

:number: Campos de tipo numérico con o sin decimales. Dispone de los atributos:

    * **decimal**: para configurar la precisión a visualizar.

    * **min** : para indicar el valor mínimo.

    * **max**: para indicar el valor máximo.

    * **step**: para indicar el aumento o decremento al realizar un “paso” mediante el control de avance/retroceso.

:money: Campos de tipo moneda o importes. Dispone de los mismos atributos que el tipo *number* para su configuración.

:checkbox: Valores booleanos que se visualizan mediante el icono de un check (true) o un guión (false) respectivamente.

:datepicker: Campos de tipo fecha, que incorporan un desplegable para elegir la misma.

:color: Para la selección de colores.

:file: Permite seleccionar y subir un archivo de nuestro equipo local al servidor.

:autocomplete: Visualiza una lista de valores a modo de "ayuda" cuando el usuario introduce un valor.
    Lista de valores se pueden cargar de manera dinámica de un modelo o mediante una lista fija de valores
    indicados en el archivo XML de la vista. Para definir los valores se utilizarán etiquetas **<values>**
    descritas dentro del grupo *<widget>*.

    * Para la carga de valores fijos se indicará para cada etiqueta *<values>* el atributo *title* y asignándole un valor.

    * Para la carga dinámica de los valores se utilizará una sóla etiqueta *<values>* indicando los atributos:

        -  *source*: Indica el nombre de la tabla origen de los datos
        -  *fieldcode*: Indica el campo que contiene el valor a grabar en el campo de la columna
        -  *fieldtitle*: Indica el campo que contiene el valor que se visualizará en pantalla

:select: Permite al usuario seleccionar una opción de entre una lista de valores preestablecidos.
    Los valores podrán ser fijos indicando la lista en el XML de la vista o dinámicos, ya sea
    calculados en base al contenido de los registros de una tabla de la base de datos o mediante la
    definición de un rango de valores. Para definir los valores se utilizarán etiquetas *<values>*
    descritas dentro del grupo *<widget>*.

    * Para la carga de valores fijos se indicará para cada etiqueta *<values>* el atributo *title* y asignándole un valor.

    * Para el caso de valores de una tabla se utilizará una sóla etiqueta *<values>* indicando los atributos:

        -  *source*: Indica el nombre de la tabla origen de los datos
        -  *fieldcode*: Indica el campo que contiene el valor a grabar en el campo de la columna
        -  *fieldtitle*: Indica el campo que contiene el valor que se visualizará en pantalla
        -  *translate*: (Opcional) Indica si hay que traducir los títulos obtenidos. **[translate=“true”]**

    * Para el caso de valores por definición de rango una sóla etiqueta *<values>* indicando los atributos:

        -  *start*: Indica el valor inicial (numérico o alfabético)
        -  *end*: Indica el valor final (numérico o alfabético)
        -  *step*: Indica el valor del incremento (numérico)


**Ejemplos:**

.. code:: xml

      <!--- AUTOCOMPLETE -->
      <widget type="autocomplete" fieldname="codsubcuenta" required="true">
          <values title="title-to-translate1">Value1</values>
          <values title="title-to-translate2">Value2</values>
          <values title="title-to-translate3">Value3</values>
      </widget>

      <widget type="autocomplete" fieldname="referencia">
          <values source="articulos" fieldcode="referencia" fieldtitle="descripcion"></values>
      </widget>

      <!--- SELECT -->
      <widget type="select" fieldname="documentacion">
          <values title="Pasaporte">PASAPORTE</values>
          <values title="D.N.I.">DNI</values>
          <values title="N.I.E.">NIE</values>
      </widget>

      <widget type="select" fieldname="codgrupo">
          <values source="gruposclientes" fieldcode="codgrupo" fieldtitle="nombre"></values>
      </widget>

      <widget type="select" fieldname="codgrupo">
          <values start="0" end="6" step="1"></values>
      </widget>


Otros atributos
^^^^^^^^^^^^^^^

Para las vistas de edición (*Edit* y *EditList*) disponemos de los siguientes atributos:

:fieldname: (Obligatorio) Nombre del campo que contiene la información.

:onclick: Nombre del controlador al que llamará y se pasará el valor del campo al hacer click sobre el valor de la columna.

:required: Atributo opcional para indicar que la columna debe tener un valor en el momento de persistir los datos en la base de datos. **[required=“true”]**

:readonly: Atributo opcional para indicar que la columna no es editable. **[readonly=“true”]**

:maxlength: Número máximo de carácteres que permite la campo.

:icon: Si se indica se visualizará el icono a la izquierda del campo.

:hint: Texto explicativo que se visualiza al colocar el ratón sobre el.


group
-----

Crea una rejilla bootstrap donde incluirá cada una de las columnas *<column>* declaradas
dentro del grupo. Se puede personalizar el grupo mediante los siguientes atributos:

:name: Identificador interno del grupo. Es obligatorio su uso. Como norma se recomienda el uso de identificadores en minúsculas y en inglés.

:title: Etiqueta descriptiva del grupo. Para los grupos **no se usará** el valor name en caso de no informarse un title.

:titleurl: URL destino si el usuario hace click sobre el título del grupo.

:icon: Si se indica se visualizará el icono a la izquierda del título. El icono de el grupo sólo se mostrará si el atributo title está presente.

:order: Posición que ocupa el grupo. Sirve para indicar el orden en que se visualizara.

:numcolumns: Fuerza el tamaño al valor indicado, usando el sistema de grid de Bootstrap
    siendo mínimo 1 y máximo 12. Si no se informa toma como valor *0* aplicando el sistema de
    tamaño automático de Bootstrap. Es importante recordar que un grupo tiene siempre 12
    columnas disponibles en su *interior*, independientemente del tamaño que tenga definido el grupo.
