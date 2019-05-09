.. highlight:: rst
.. title:: Facturascripts, Clase AssetManager, personalizar CSS y JavaScript
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Gestión de Assets. Hojas de estilo CSS y código JavaScript
  :keywords: facturascripts, documentacion, desarrollo, assetmanager, personalizar, css, js, javascript
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: AssetManager FacturaScripts
  :lang: es


############
AssetManager
############

La clase AssetManager permite añadir archivos CSS y JavaScript personalizados a la página.
El archivo indicado se agregará a la lista de archivos del mismo tipo.

La estructura a mantener dentro de nuestros plugins es la de crear una carpeta **Assets** en el
raíz del plugin, dentro de la cual crearemos las carpetas CSS y/o JS, donde tendremos
los archivos según las necesidades.


Cargar archivos propios
=======================

Como se ha comentado, los archivos personalizados deben ir dentro *Assets* en su carpeta según el tipo.
Los archivos de JavaScript que tienen el mismo nombre que el controlador (por ejemplo: *ListProducto*) se
cargan automáticamente por lo que no se necesita añadirlos al proceso de carga.

Si deseamos añadir una nueva hoja de estilo o un archivo JavaScript con un nombre distinto al controlador
debemos ejecutar el método estático **add** de la clase AssetManager, indicando el tipo y la ruta.
Es posible indicarle el nivel de prioridad que debe darse a la carga mediante un valor numérico.

.. code:: php

    AssetManager::add('css', FS_ROUTE . '/Plugins/webportal/node_modules/spectre.css/dist/spectre.min.css', 3);
    AssetManager::add('js', FS_ROUTE . '/Plugins/MiPlugin/Assets/JS/MyJs.js', 3);
