.. title:: Views
.. highlight:: rst

.. title:: Facturascripts desarrollo de vistas
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Diseño de vistas mediante plantilla TWIG
  :keywords: facturascripts, diseño, vista, twig, herencia, desarrollo


######
Vistas
######

Es la parte encargada del visionado en pantalla de todos los elementos con los que
el usuario va interactuar. Es decir, la información de los modelos, los mensajes para
el usuario, botones para las acciones, formularios modales, etc.

*Facturascripts 2018* utiliza el motor de plantillas `TWIG <https://twig.symfony.com>`_, un motor realmente
muy potente que nos permite el uso tanto de código HTML como de variables, bucles, bloques,
macros y el uso de datos declarados en el controlador.

Los archivos de vistas siempre deben tener la extensión *.html.twig*, utilizar la nomenclatura
`UpperCamelCase <https://es.wikipedia.org/wiki/CamelCase>`_ y se encuentran en la carpeta *View*.

Como norma general las nuevas vistas deben heredar de *Master/MenuTemplate.html.twig*, que es la vista que
incluye la estructura básica así como el menú superior. Si por el contrario no queremos el menú,
podemos heredar de *Master/MicroTemplate.html.twig*, una versión más sencilla de modelo.

Ejemplo: *MyView.html.twig*

.. code:: php

    {% extends 'Master/MenuTemplate.html.twig' %}

    {% block body %}
    <h1>Hola mundo</h1>
    {% endblock %}


Seleccionar una vista
=====================

La aplicación siempre "funciona" desde un controlador, ya sea desde las opciones de menú
como desde las acciones de los botones, y éste es el encargado de seleccionar la vista
que mostrará el resultado del proceso seleccionado. Para seleccionar la vista se utiliza
el método *setTemplate* indicando el nombre de la vista sin incluir la extensión.

.. code:: php

  $this->setTemplate('MyView');


Acceso al controlador
=====================

Como se ha comentado anteriormente, desde la vista o plantilla podemos acceder a la información
del controlador. Este "acceso" debe ser unidireccional, es decir sólo debemos leer datos del
controlador y no cambiar los valores para evitar confusiones y simplificar el seguimiento del
código. A todos los efectos, debemos entender que la representación de la vista es lo último que
la aplicación realiza antes de trasmitir el control al usuario.


fsc
---

Para acceder a la información del controlador usaremos la variable *fsc* que es un "acceso" al objeto
instanciado del controlador. Esto significa que podemos acceder a todos los métodos y variables
declarados como *public*. Puede encontrar más información en el apartado `Controladores <Controllers>`.


i18n
----

Nos permite acceder al gestor de traducciones. Esto resulta esencial para poder mostrar
en las vistas los textos y etiquetas en el idioma que usuario tiene seleccionado.


log
---

Esta variable nos da acceso al sistema de registro de mensajes tanto al usuario como mensajes
de depuración.


appSettings
-----------

Para acceder de manera rápida y sencilla a los valores de configuración o preferencias de la aplicación.


controllerName
--------------

Contiene el nombre del controlador que se está ejecutando.


template
--------

Contiene el nombre de la plantilla cargada.


Uso de TWIG
===========

Puede encontrar toda la documentación en la `página oficial de TWIG <https://twig.symfony.com/doc/2.x>`_.

Acceso a métodos y variables
----------------------------

.. code:: php

    {{ fsc.url() }}   /// url de la página que se ejecuta

    {{ fsc.user.nick }}   /// nombre del usuario


Condicional IF
--------------

.. code:: php

      {% if kenny.sick %}
        Kenny is sick.
      {% elseif kenny.dead %}
        You killed Kenny! You bastard!!!
      {% else %}
        Kenny looks okay --- so far
      {% endif %}


Bucles FOR
----------

.. code:: php

      {% for user in users %}
        <li>{{ user.username|e }}</li>
      {% else %}
        <li><em>no user found</em></li>
      {% endfor %}
