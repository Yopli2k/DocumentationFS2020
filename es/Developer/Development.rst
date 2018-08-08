.. highlight:: rst
.. title:: Facturascripts, conceptos generales para el desarrollo
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación de ayuda para el desarrollo de Facturascripts 2018
  :keywords: facturascripts, documentacion, desarrollo, plugin, conceptos


###################
Conceptos Generales
###################

Antes de que empiece a programar o modificar el código de FacturaScripts, es necesario
que establecer algunos conceptos. Continuando con el patrón MVC (Modelo, Vista y
Controlador) iniciado por la versión anterior de *FacturaScripts* los controladores
extendidos añaden la posibilidad de definir nuestros modelos y controladores de manera
sencilla, incluyendo, a las vistas tradicionales de *FS2015* un nuevo concepto,
las vistas XML.

`Modelos <Models>`_:
    **Son los encargados de gestionar los datos**, estableciendo la estructura básica
    de cada registro de datos y los métodos para leer, modificar y borrar dichos datos.

`Vistas <Views>`_:
    **Indican la estructura de "pintado o visionado" en pantalla**. No sólo visualizan los datos
    de los modelos, también definen acciones, mensajes para el usuario, formularios modales, etc.

`Controladores <Controllers>`_:
    **Realizan las tareas solicitadas por el usuario**, haciendo de intermediario
    entre la vista o interface del usuario y los datos almacenados en la base de datos.


Normas de aplicación
====================

- **Sus personalizaciones van en plugins**:
    No deben realizarse cambios en los archivos del Core o Kernel de *Facturascripts*.
    Esto es así por dos motivos principales. Cualquier cambio se perderá al actualizar
    y porque es muy importante poder mantener la instalación actualizada.
    Coloque sus personalizaciones a modo de plugin dentro de la carpeta *Plugins*.


- **Nomenclatura de archivos y clases**:
    Para nombrar tanto los archivos como las clases que se declaran se utiliza el sistema
    `UpperCamelCase <https://es.wikipedia.org/wiki/CamelCase>`_. Es decir, todo en minúsculas
    con la excepción de la primera letra de cada palabra y sin separador entre palabras.
    El nombre del archivo debe ser en singular, y debe coincidir con el nombre de la clase
    que declara, declarando una única clase por archivo.


- **Espacios de nombres**:
    Cada clase debe estar en el espacio de nombre correspondiente a su carpeta. De la misma
    manera, cada plugin tiene su espacio de nombre reservado que se corresponde con
    *FacturaScripts/Plugins/{Nombre del Plugin}*


Creación de Plugins
===================

Un plugin es un conjunto de archivos que añaden nuevas funcionalidades la instalación de
*FacturaScripts*. Las personalizaciones pueden ser muy básicas, como añadir nuevos campos
a modelos ya existentes, como añadir nuevos procesos y tareas.
Para crear un plugin, debemos crear una carpeta con el nombre del plugin dentro de la carpeta *Plugins*,
donde iremos incorporando los archivos necesarios y clases necesarias para la nueva
personalización. La carpeta del plugin debe tener la siguiente estructura de directorios:

  - **Controller**: Archivos de controladores nuevos o heredados.

  - **Model**: Archivos de modelos nuevos o heredados.

  - **Table**: Archivos con la definición en xml de las nuevas tablas de la base de datos.

  - **View**: Archivos con las plantillas de visualización.

  - **XMLView**: Archivos con las definiciones de las vistas xml (*ExtendedControllers*).

  - **facturascripts.ini**: Archivo de declaración y configuración del plugin.


Archivo facturascripts.ini
--------------------------

Este archivo es el encargado de la declaración y configuración del plugin, por lo porque
resulta imprescindible. El archivo debe contener los siguientes valores:

:name: Nombre del plugin y de la carpeta que lo contiene.
:description: Descripción del plugin. Debe ser suficientemente descriptiva para el usuario.
:version: Número de versión del plugin. Se utiliza para el control de actualizaciones.
:min_version: Indica la versión mínima de FacturaScripts necesaria para su instalación.
:require: Permite indicar una lista de plugins (separadas por coma) de los que depende este plugin.


Ejemplo: *plugin Community, versión 1 y requiere FS2018 con webportal*

.. code:: ini

    name = 'Community'
    description = 'Community management'
    version = 1
    min_version = 2018
    require = 'webportal'
