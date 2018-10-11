.. title:: XML Rows
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas. Configuración de rows
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de rows en vistas XML.
  :keywords: facturascripts, documentacion, diseño, rows, card, vista, xml, desarrollo


################
Vistas XML: Rows
################

Etiqueta rows
=============

Este grupo permite añadir funcionalidad a cada una de las filas o añadir
filas con procesos especiales. Así mediante la etiqueta *<row>* podemos
ir añadiendo las funcionalidades, de manera única y mediante el atributo *type*
indicar la acción que realiza, teniendo cada tipo unos requerimientos propios.

.. warning::

  El tipo (*type*) del row se utiliza como clave de identificación por lo que no
  podemos incluir dos veces el mismo tipo. En caso de indicar el mismo tipo más
  de una vez sólo se procesará el último.


Relación de Colores
-------------------
Para la selección o aplicación del color se utilizan los colores para tablas de bootstrap.

.. sidebar:: Colores (Rows)

    .. image:: images/es/rows-colors.png

:primary: azul
:secundary: gris
:success: verde
:danger: rojo
:warning: amarillo
:info: verde-azul
:light: gris claro (muy claro)
:dark: gris oscuro


status
======

Este tipo permite colorear las filas en base al valor de un campo del registro o
de una serie de condiciones. Se declara mediante la inclusión de una relación de
uno o varios registros *<option>* indicando la configuración que se aplicará para la fila.

Para la aplicación del *option* se tiene que declarar cuatro elementos:

    - El nombre del campo
    - El operador
    - El valor con el que se compara el campo
    - El color a aplicar en caso de cumplirse la condición


Relación de Operadores
----------------------

Para establecer el operador se comprueba el primer carácter del valor de la etiqueta *option*.

:>: Se aplicará si el valor del campo del modelo es mayor que el valor indicado.
:<: Se aplicará si el valor del campo del modelo es menor que el valor indicado.
:!: Se aplicara si el valor del campo del modelo es diferente que el valor indicado.

En cualquier otro caso se realizará una comprobación de igualdad, es decir que el
valor del campo del modelo es igual al valor indicado.


Declaración de las condiciones
------------------------------

Para la declaración de condiciones se puede utilizar alguno de los siguientes métodos:

:Un único campo: se declara el atributo **fieldname** dentro de la declaración del **<row>**
    indicando el nombre del campo que contendrá los valores a comprobar para el pintado.

:Varios campos: se declara el atributo **fieldname** dentro de la declaración del **<option>**
    indicando el nombre del campo que contendrá los valores a comprobar para el pintado.

:Ambos: se declara el atributo **fieldname** dentro de **<row>** y dentro de los **<option>**
    que no usen el campo general indicado dentro de *<row>*.


Ejemplos:

*Para condiciones con un mismo campo*

- *Pinta la fila de color "info" si el campo* ``estado`` *es* ``Pendiente``

- *Pinta la fila de color "warning" si el campo* ``estado`` *es* ``Parcial``

.. code:: xml

        <rows>
            <row type="status" fieldname="estado">
                <option color="info">Pendiente</option>
                <option color="warning">Parcial</option>
            </row>
        </rows>


*Para condiciones con distintos campos y valores*

- *Pinta la fila de color "info" si el campo* ``nostock`` *es* ``Verdadero``

- *Pinta la fila de color "danger" si el campo* ``bloqueado`` *es* ``Verdadero``

- *Pinta la fila de color "success" si el campo* ``stockfis`` *es mayor de* ``0``

- *Pinta la fila de color "warning" si el campo* ``stockfis`` *es menor de* ``1``

.. code:: xml

        <rows>
            <row type="status">
                <option color="info" fieldname="nostock">1</option>
                <option color="danger" fieldname="bloqueado">1</option>
                <option color="success" fieldname="stockfis">&gt;0</option>
                <option color="warning" fieldname="stockfis">&lt;1</option>
            </row>
        </rows>


statistics
==========

Permite definir una lista de botones o etiquetas estadísticas que dan información al usuario
calculados al momento por el controlador y pudiendo consultar al hacer click.
La declaración de las etiquetas se realiza de manera similar a lo descripto en el apartado
`botones <XMLButtons>`__ con la salvedad de que no es necesaria la etiqueta *column*.
A modo de resumen de las propiedades:

:id: identificador html para poder selecionarlo desde JavaScript.
:icon: icono que se visualizará a la izquierda de la etiqueta.
:label: texto o etiqueta que se visualizará en el botón. **Se traducirá automáticamente**.
:function: nombre de la función del controlador que se ejecuta para calcular el texto a visualizar.
:link: URL destino o función JavaScript, donde se redigirá al usuario al hacer click sobre el botón. (Opcional)


Ejemplo:

.. code:: xml

        <rows>
            <row type="statistics">
                <button icon="fa-files-o" label="Alb. Pdtes:" function="nombre_function" link="#url"></option>
                <button icon="fa-files-o" label="Pdte Cobro:" function="nombre_function" link="#url"></option>
            </row>
        </rows>


actions
=======

Permite definir un grupo de botones que se visualizarán dependiendo del tipo de controlador
en la cabecera junto al resto de botones de la pestaña (*ListController) o en el pié del
formulario de edición entre los botones de eliminar y grabar (*EditController*).
La declaración de los botones se realiza de manera similar a lo descripto en el apartado
`botones <XMLButtons>`__ con la salvedad de que no es necesaria la etiqueta *column*.

A modo de resumen de las propiedades:

:type: indica el tipo de botón o acción.

    - **action**: al hacer clic se recargará la página ejecutando el action indicado en el atributo ``action``.
        Este action deberá estar implementado en el controlador.

    - **modal**: al hacer clic mostrará el modal con el nombre indicado en el atributo ``action``.

    - **js**: al hacer clic ejecutará la función javascript indicada en el atributo ``action``.


:id: identificador html para poder selecionarlo desde JavaScript.
:icon: icono que se visualizará a la izquierda de la etiqueta.
:label: texto o etiqueta que se visualizará en el botón.
:color: indica el color del botón, según las relación de colores antes indicada.
:hint: ayuda que se muestra al usuario al poner el puntero del ratón sobre el botón.
:action: indica la acción que se envía al controlador o a la función JavaScript.


Ejemplo:

.. code:: xml

        <rows>
            <row type="actions">
                <button type="action" label="vat-register" color="info" action="register" hint="hint-vat-register" icon="fa-book" />
                <button type="action" label="clone" color="info" action="clone" hint="clone-account-entry" icon="fa-clone" />
                <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
            </row>
        </rows>


header y footer
===============

Permite añadir información adicional a visualizar al usuario en la cabecera y/o el pie de la vista.
La información se muestra en forma de paneles o fichas ("cards" de Bootstrap) donde podemos
incluir mensajes y botones tanto de acción como modales. Para declarar un panel usaremos
la etiqueta *<group>* en la que incluiremos etiquetas *button* (si los necesitamos).
Podemos personalizar cada uno de los apartado del panel como la cabecera, el cuerpo
y/o el pie con atributos:

:name: establece el identificador para el panel.
:numcolumns: establece el tamaño del card. Si no se indica se aplicará tamaño automático.
:title: indica un texto para la cabecera del panel.
:label: indica un texto para el cuerpo del panel.
:footer: indica un texto para el pie del panel.
:html: incluye una plantilla twig en el contenido del panel.
:class: añade las clases CSS indicadas al panel. Ejemplos:

    - Se puede indicar ``text-color`` para establecer el color del texto.
    - Se puede indicar ``border-color`` para establecer el color de los bordes del panel.


Ejemplos:

*Cabecera de vista*

.. code:: xml

        <row type="header">
            <group name="footer1" footer="specials-actions" label="Esto es una muestra de botones en un 'bootstrap card'">
                <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
                <button type="action" label="Action" color="info" action="process1" icon="fa-book" hint="Ejecuta el controlador con action=process1" />
            </group>
        </row>


*Pie de vista*

.. code:: xml

        <row type="footer">
            <group name="actions">
                <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
                <button type="action" label="create-accounting-entry"
                        color="danger" action="create-accounting-entry"
                        hint="hint-create-accounting-entry" icon="fa-balance-scale" />
            </group>

            <group name="help" class="collapse show" html="Block/Info.html.twig"></group>

            <group name="summary" html="Block/Resumen.html.twig"></group>
        </row>

        <row type="footer">
            <group name="footer1" footer="specials-actions" label="Esto es una muestra de botones en un 'bootstrap card'">
                <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
                <button type="action" label="Action" color="info" action="process1" icon="fa-book" hint="Ejecuta el controlador con action=process1" />
            </group>
        </row>
