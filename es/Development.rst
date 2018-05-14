.. title:: Development
.. highlight:: rst

.. title:: Facturascripts, desarrollar nuevos plugins, adaptaciones y personalizaciones
.. meta::
   :description: Documentación de usuario y ayuda para el desarrollo de Facturascripts 2018
   :keywords: facturascripts, documentacion, desarrollo, plugin, adaptaciones, personalizaciones


##########
Desarrollo
##########

En *Facturascripts 2018* se ha realizado un gran esfuerzo para simplificar todo
el proceso personalización de la aplicación. Las tareas de creación de nuevas opciones
y desarrollos son realmente sencillas y no requieren de grandes conocimientos en
programación ni diseño HTML gracias a los controladores extendidos.

.. note::

  Debido al gran cambio en la metodología de creación de personalizaciones, es muy
  importante familiarizarse con el sistema antes de iniciar cualquier nuevo plugin.
  Esto nos evitará problemas y errores de diseño que pueden llevar a una mala experiencia
  a la hora de desarrollar.

Continuando con el patrón MVC (Modelo, Vista y Controlador) iniciado por la versión
anterior de *FacturaScripts* los controladores extendidos añaden la posibilidad
de definir nuestros modelos y controladores de manera sencilla, incluyendo,
a las vistas tradicionales de *FS2015* un nuevo concepto, las vistas XML.

- `Modelos <Models>`_: **Son los encargados de gestionar los datos**, estableciendo la estructura básica
    de cada registro de datos y los métodos para leer, modificar y borrar dichos datos.


- `Vistas <Views>`_: **Indican la estructura de "pintado o visionado" en pantalla**. No sólo visualizan los datos
    de los modelos, también definen acciones, mensajes para el usuario, formularios modales, etc.


- `Controladores <Controllers>`_: **Realizan las tareas solicitadas por el usuario**, haciendo de intermediario
    entre la vista o interface del usuario y los datos almacenados en la base de datos.
