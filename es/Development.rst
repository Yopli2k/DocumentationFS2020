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


Conceptos Generales
===================

Antes de que empiece a programar o modificar el código de FacturaScripts, es necesario
que establecer algunos conceptos.

- **Sus personalizaciones van en plugins**:
  No deben realizarse cambios en los archivos del Core o Kernel de *Facturascripts*.
  Esto es así por dos motivos principales. Cualquier cambio se perderá al actualizar
  y porque es muy importante poder mantener la instalación actualizada.
  Coloque sus personalizaciones a modo de plugin dentro de la carpeta *Plugins*.

- **Nomenclatura de archivos y clases**:
  Para nombrar tanto los archivos como las clases que se declaran se utiliza el sistema
  `UpperCamelCase <https://es.wikipedia.org/wiki/CamelCase>`. Es decir, todo en minúsculas
  con la excepción de la primera letra de cada palabra y sin separador entre palabras.
  El nombre del archivo debe ser en singular, y debe coincidir con el nombre de la clase
  que declara, declarando una única clase por archivo.

- **Espacios de nombres**:
  Cada clase debe estar en el espacio de nombre correspondiente a su carpeta. De la misma
  manera, cada plugin tiene su espacio de nombre reservado que se corresponde con
  *FacturaScripts/Plugins/{Nombre del Plugin}*
