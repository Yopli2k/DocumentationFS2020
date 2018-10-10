.. title:: XML Buttons
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas. Declaración de botones
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de botones en vistas XML.
  :keywords: facturascripts, documentacion, diseño, button, boton, vista, xml, desarrollo


###################
Vistas XML: Buttons
###################


button
------

Este elemento visual está disponible sólo en vistas de tipo *Edit* y *EditList* y en
las fichas de información que se definen en el grupo *rows*. Como su nombre indica permite
incluir un botón en una de las columnas de edición. Existen tres tipos de botones declarados
mediante el atributo ``type`` y con funciones distintas:

-  **calculate** : Botón para mostrar un cálculo estadístico. Es exclusivo del grupo *<rows>* y se detalla más adelante.

-  **action** : Botón para ejecutar una acción en el controlador o una función JavaScript.

-  **modal** : Botón para mostrar un formulario modal.

Podemos personalizarlos mediante los atributos:

:type: indica el tipo de botón.
:id: identificador html para poder selecionarlo desde JavaScript.
:icon: icono que se visualizará a la izquierda de la etiqueta.
:label: texto o etiqueta que se visualizará en el botón.
:color: indica el color del botón, según los colores de Bootstrap para botones.
:hint: ayuda que se muestra al usuario al poner el puntero del ratón sobre el botón.
  Esta opción sólo está disponible para botones del tipo ``action``.
:action: esta propiedad varía según el tipo. Para botones ``action`` indica la acción
  que se envía al controlador, para que éste realice algún tipo de proceso especial.
  Para botones de tipo ``modal`` indica el formulario modal que se debe mostrar al usuario.
:onclick: Para el tipo ``action`` permite establecer el método JavaScript que se llamará al hacer click.
  Para el tipo ``calculate`` permite establecer la URL de llamada al hacer click.
:function: (Sólo para botones ``calculate``) Establece el método del controlador PHP que calcula el contenido del botón.

Ejemplo:

.. code:: xml

      <column name="action1" order="100">
          <button type="action" label="Action" color="info" action="process1" icon="fa-book" hint="Ejecuta el controlador con action=process1" />
      </column>

      <column name="action2" order="100">
          <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
      </column>
