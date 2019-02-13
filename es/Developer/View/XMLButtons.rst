.. title:: XML Buttons
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas. Declaración de botones
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de botones en vistas XML.
  :keywords: facturascripts, documentacion, diseño, button, boton, vista, xml, desarrollo
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Vistas Botones FacturaScripts
  :lang: es


###################
Vistas XML: Buttons
###################


button
======

Como su nombre indica permite incluir un botón en una de columna de edición, en la
zona de acciones del formulario de edición o en paneles informativos (tanto de cabecera
como de pie de las vistas). Existen varios tipos de botones declarados mediante el
atributo ``type`` según la función que realizará el botón al hacer click o seleccionarlo:

-  **action** : Botón para ejecutar una acción en el controlador. Al hacer clic se
    recargará la página ejecutando el action indicado en el valor del atributo action.
    Este action deberá estar implementado y gestionado en el controlador.

-  **link** : Botón para abrir una url, normalmente externa a la aplicación.

-  **modal** : Botón para mostrar un formulario modal. Al hacer clic mostrará el formulario
    modal con el nombre indicado en el valor del atributo action.

-  **js** : Botón para ejecutar un método/código JavaScript. Al hacer clic ejecutará
    lo indicado en el valor del atributo action.


Relación de Colores
-------------------
Para la selección o aplicación del color se utilizan los colores para botones de bootstrap.

.. sidebar:: Colores (Buttons)

    .. image:: images/buttons-colors.png

:primary: azul
:secundary: gris
:success: verde
:danger: rojo
:warning: amarillo
:info: verde-azul
:light: gris claro
:dark: negro
:link: sólo texto


Atributos y Personalización
---------------------------

Podemos personalizarlos mediante los atributos:

:type: indica el tipo de botón (según lo descrito anteriormente).
:id: identificador html para poder selecionarlo desde JavaScript.
:icon: icono que se visualizará a la izquierda de la etiqueta.
:label: texto o etiqueta que se visualizará en el botón.
:level: Sólo los usuarios con un nivel igual o superior verán el botón. Por defecto 0.
:color: indica el color del botón, según los colores de Bootstrap para botones.
:hint: ayuda que se muestra al usuario al poner el puntero del ratón sobre el botón.
:function: (Sólo para botones estadísticos) Establece el método del controlador PHP que calcula el contenido del botón.
:action: esta propiedad varía según el tipo.

    - Para botones ``action`` indica la acción que se envía al controlador.

    - Para botones de tipo ``link`` indica la url destino.

    - Para botones de tipo ``modal`` indica el nombre del formulario modal que se debe mostrar al usuario.

    - Para botones de tipo ``js`` indica el código o función JavaScript que se debe ejecutar.


.. important::

  El atributo **id** debe tener un valor único para todo el html de la página.
  Es responsabilidad del desarrollador cumplir con las normas de HTML5 en referencia
  a los identificadores únicos.


Ejemplo:

.. code:: xml

      <column name="action1" order="100">
          <button type="action" label="Action" color="info" action="process1" icon="fa-book" hint="Ejecuta el controlador con action=process1" />
      </column>

      <column name="action2" order="100">
          <button type="modal" label="Modal" color="primary" action="test" icon="fa-users" />
      </column>
