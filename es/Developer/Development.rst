.. highlight:: rst
.. title:: Facturascripts, desarrollo de adaptaciones y personalizaciones
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación de ayuda para el desarrollo de Facturascripts 2018
  :keywords: facturascripts, documentacion, desarrollo, plugin, adaptaciones, personalizaciones
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Desarrollo FacturaScripts
  :lang: es


###################
Conceptos Generales
###################

En *Facturascripts 2018* se ha realizado un gran esfuerzo para simplificar todo
el proceso personalización de la aplicación. Las tareas de creación de nuevas opciones
y desarrollos son realmente sencillas y no requieren de grandes conocimientos en
programación ni diseño HTML gracias a los controladores extendidos.

.. important::

  Debido al gran cambio en la metodología de creación de personalizaciones, es muy
  importante familiarizarse con el sistema antes de iniciar cualquier nuevo plugin.
  Esto nos evitará problemas y errores de diseño que pueden llevar a una mala experiencia
  a la hora de desarrollar.

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

Un plugin es un conjunto de archivos con una estructura concreta que añaden nuevas
funcionalidades la instalación de *FacturaScripts*. Estas personalizaciones pueden ser muy básicas,
como añadir nuevos campos a modelos ya existentes, o más elaboradas como añadir nuevos procesos y tareas.
Para crear un plugin, debemos crear una carpeta con el nombre del plugin dentro de la carpeta *Plugins*,
donde iremos incorporando los archivos necesarios y clases necesarias para la nueva
personalización. La carpeta del plugin debe tener la siguiente estructura de directorios:

  - **Controller**: Archivos de controladores nuevos o heredados.

  - **Model**: Archivos de modelos nuevos o heredados.

  - **Table**: Archivos con la definición en xml de las nuevas tablas de la base de datos.

  - **View**: Archivos con las plantillas de visualización.

  - **XMLView**: Archivos con las definiciones de las vistas xml (*ExtendedControllers*).

  - **Lib**: Archivos con para procesos especiales o librerías de agrupación de código/utilidades.

  - **facturascripts.ini**: Archivo de declaración y configuración del plugin.

  - **Init.php**: Archivo opcional donde se definen procesos automáticos.


Archivo facturascripts.ini
--------------------------

Este archivo es el encargado de la declaración y configuración del plugin, por lo porque
resulta imprescindible. El archivo debe contener los siguientes valores:

:name: Nombre del plugin y de la carpeta que lo contiene. **Deben coincidir el nombre con la carpeta**.
:description: Descripción del plugin. Debe ser suficientemente descriptiva para el usuario.
:version: Número de versión del plugin. Debe ser un número entero o decimal. Se utiliza para el control de actualizaciones.
:min_version: Indica la versión mínima de FacturaScripts necesaria para su instalación.
:require: Permite indicar una lista de plugins (separadas por coma) de los que depende este plugin.

Ejemplo: *plugin Community, versión 1 y requiere FS2018 con webportal*

.. code:: ini

    name = 'Community'
    description = 'Community management'
    version = 1
    min_version = 2018.005
    require = 'webportal'


Archivo Init.php
----------------

Los plugins pueden contener este archivo, con la declaración de la clase **Init** que debe
heredar de la clase base *InitClass*, en el que se definen procesos a ejecutar cada vez que
carga FacturaScripts, cuando se instala o cuando se actualiza el plugin.

.. code:: php

    namespace FacturaScripts\Plugins\MyNewPlugin;

    use FacturaScripts\Core\Base\InitClass;

    class Init extends InitClass
    {

            public function init()
            {
                // Se ejecuta cada vez que carga FacturaScripts (si este plugin está activado).
            }

            public function update()
            {
                // Se ejecuta cada vez que se instala o actualiza el plugin
            }
    }


Usar otros frameworks
---------------------

Si lo necesita puede incluir otros frameworks en su plugin, mediante composer. La forma
en que estos se carguen automáticamente es añadir **require** al *autoload.php* justo después
del namespace en el *Init.php*.

.. code:: php

    namespace FacturaScripts\Plugins\MyNewPlugin;

    require_once __DIR__ . '/vendor/autoload.php';

    use FacturaScripts\Core\Base\InitClass;

    class Init extends InitClass
    {
        [ ... ]
    }
