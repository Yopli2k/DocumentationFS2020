.. highlight:: rst
.. title:: Facturascripts, Clase AppSettings, las preferencias de la aplicacion
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Documentación de ayuda para el desarrollo de Facturascripts 2018
  :keywords: facturascripts, documentacion, desarrollo, appsettings, preferencias


###########
AppSettings
###########

La clase AppSettings permite conocer y establecer algunos comportamientos de la aplicacion
mediante valores a utilizar por defecto para distintas situaciones de la aplicación.
A la hora de trabajar con estos valores debemos diferenciar tres métodos:

    - Definición y modificación visual de los valores por defecto desde la página.

    - Acceso y modificación desde un controlador.

    - Acceso desde una planilla de twig.


La información indicada para estos valores por defecto es almacenada en la tabla **settings**.
Aunque a priori es accesible por el modelo del mismo nombre, y mediate la propiedad *properties*
que es un array con la estructura *nombre del campo => valor del campo*, **no se recomienda**
ese método de acceso sino el uso de los métodos de la clase *AppSettings* desde el controlador (Ver más adelante).


Preferencias de la aplicación
=============================

En esta página, ubicada en el menú (:guilabel:`Administrador->Panel de Control->Preferencias de aplicación`),
los valores se agrupan en pestañas según el plugin o grupo de datos al que pertenecen.

El controlador que lo gestiona es EditSettings, un controlador extendido que hereda de PanelController,
lo que significa que usa las vistas xml para su diseño, donde el nombre del archivo xml
debe empezar por el prefijo **Settings** seguido del nombre del apartado que deseamos agregar
a EditSettings. La carga de las distintas pestañas que se visualizan en EditSettings se
realiza de manera automática no necesitando controladores adicionales para gestionar
el tratamiento de los settings de nuestro plugin.

.. code::

   default -> SettingsDefault.xml
   email -> SettingsEmail.xml
   logs -> SettingsLog.xml

   myplugin -> SettingsMyPlugin.xml


Al definir el archivo settings de la vista XML usaremos las normas de columnas y grupos
como se vió en el apartado `columnas <XMLColumns>`__, pudiendo añadir botones de accion para acciones
especiales y footers y/o headers si fuera necesario (`rows <XMLRows>`__). Para el caso de añadir botones de acciones
necesitaríamos crear un controlador dentro de nuestro plugin heredando de EditSettings donde
implementaremos las acciones especiales deseadas.

.. code:: php

    class EditMySettings extends EditSettings
    {
        protected function execAfterAction($action)
        {
            switch ($action) {
                case 'my-action':
                    [ ... ]
                    break;

                default:
                    parent::execAfterAction($action);
                    break;
            }
        }
    }


.. AppSettings-Controller

Acceso desde Controlador
========================

get
---
Para acceder a un valor por defecto usaremos el método estático **get** de la clase *AppSettings*.
Este método necesita que le indiquemos el grupo o nombre del plugin que contiene el valor
que deseamos. También podemos indicar un valor por defecto por si no existe el campo en el grupo.
El mismo nombre de campo/valor puede estar en más de una grupo o plugin, por lo conviene indicar
correctamente el nombre del grupo.


.. code:: php

    $coddivisa = AppSettings::get('default', 'coddivisa');


set
---
Para establecer un valor por defecto o cambiar el valor que se ha leído del modelo *settings*
guardado con anterioridad, usaremos el método **set** de la clase *AppSettings*.
Este método necesita que le indiquemos el grupo o nombre del plugin que contiene el valor
que deseamos. El mismo nombre de campo/valor puede estar en más de una grupo o plugin,
por lo conviene indicar correctamente el nombre del grupo.


.. code:: php

    $appSettings = new AppSettings();
    $appSettings->set('default', 'homepage', 'AdminPlugins');


.. note::

    Si queremos que el cambio de valor sea permanente debemos llamar al método **save** de
    la misma clase, en caso contrario el nuevo valor se perderá al cargar otras páginas.


Acceso desde vista TWig
=======================
Para acceder a los valores por defecto desde una plantilla o vista de Twig simplemente usaremos
la variable **appSettings** que es un objeto de la clase AppSettings. Eso significa que tenemos
acceso a los métodos de lectura y escritura de valores definidos en el apartado de *Acceso desde Controlador*.

.. code:: twig

    {% set codpais = appSettings.get('default','codpais','ESP') %}

    {% if appSettings.get('default', 'ventasinstock', false) %}
        [ ... ]
    {% endif %}
