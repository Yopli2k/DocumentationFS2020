.. highlight:: rst
.. title:: Archivo Init.php
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Configuraciones especiales de la instalación.
  :keywords: facturascripts, configurar, init
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Archivo Init.php
  :lang: es

################
Archivo Init.php
################

Los plugins pueden contener este archivo, con la declaración de la clase **Init** que debe
heredar de la clase base *InitClass*, en el que se definen procesos a ejecutar cada vez que
carga *FacturaScripts*, cuando se instala o cuando se actualiza el plugin.

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
=====================

Si lo necesita puede incluir otros frameworks en su plugin, debe realizarse mediante **Composer**.
La forma en que estos se carguen automáticamente es añadir **require** al *autoload.php* justo después
del namespace en el *Init.php*.

.. code:: php

  namespace FacturaScripts\Plugins\MyNewPlugin;

  require_once __DIR__ . '/vendor/autoload.php';

  use FacturaScripts\Core\Base\InitClass;

  class Init extends InitClass
  {
      [ ... ]
  }
