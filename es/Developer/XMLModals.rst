.. title:: XML Modals
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas. Formularios modales
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Nuevo sistema para diseño de formularios modales en vistas XML.
  :keywords: facturascripts, documentacion, diseño, formulario, modal, vista, xml, desarrollo


##################
Vistas XML: Modals
##################

Etiqueta modals
===============

Los formularios modales son vistas complementarias a la vista principal, que permanecen
ocultas hasta que son necesarias para la realización de una tarea específica. Estos formularios
se declaran de manera muy similar a lo detallado en la sección `columnas <XMLColumns>`__.

Para crear un formulario modal, debemos incluir una etiqueta *group* con un identificador *name* único.
Dentro de este grupo podemos definir y personalizar las columnas que necesitemos, pero no se pueden crear
nuevos grupos como se podía en la sección `columnas <XMLColumns>`__.

Podemos declarar todos los formularios modales que necesitemos, declarando distintas etiquetas *group* dentro
del grupo *modals*, y respetando la unicidad de sus identificadores. Para mostrar cualquiera de los formularios
modales declarados, tendremos que definir un botón de tipo modal en la vista principal, ya sea en una columna o
en un *row* de tipo ``actions`` o ``footer``, donde el atributo ``action`` del *button* sea igual al identificador
del formulario modal.

El formulario modal mostrará la relación de columnas declaradas junto con unos botones de ``Aceptar`` y ``Cancelar``
para que el usuario pueda confirmar o cancelar el proceso a realizar.

Ejemplo:

.. code:: xml

        <modals>
            <group name="test" title="other-data" icon="fa-users">
                <column name="name" numcolumns="12" description="desc-custommer-name">
                    <widget type="text" fieldname="nombre" required="true" hint="desc-custommer-name-2" />
                </column>

                <column name="create-date" numcolumns="6">
                    <widget type="datepicker" fieldname="fechaalta" readonly="true" />
                </column>

                <column name="blocked-date" numcolumns="6">
                    <widget type="datepicker" fieldname="fechabaja" />
                </column>

                <column name="blocked">
                    <widget type="checkbox" fieldname="debaja" />
                </column>
            </group>
        </modals>
