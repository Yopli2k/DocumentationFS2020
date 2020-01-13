.. highlight:: rst
.. title:: Facturascripts, Clase EventManager, el gestor de eventos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Gestior de Eventos en modelos
  :keywords: facturascripts, documentacion, desarrollo, eventmanager, eventos, gestor
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: EventManager FacturaScripts
  :lang: es


############
EventManager
############

.. warning::
    *OBSOLETO*: El gestor de eventos de FacturaScripts ha sido sustituido por extensiones.
    El desarrollo existente con este sistema será eliminado o dejado de soportar en futuras
    versiones de FacturaScripts.


*FacturaScripts* incluye un sencillo gestor de eventos que lo dota de un mayor nivel de personalización
en el tratamiento de procesos con la información.


Eventos en modelos
==================

Todos los modelos invocan eventos al guardar o eliminar. El identificador del evento se define
mediante la cadena **Model:NombreDelModelo:accion**, y en concreto, los eventos/acciones disponibles son:

:delete: se invoca cada vez que se elimina un registro de un modelo.
:saveInsert: se invoca cada vez que se inserta un nuevo registro en el modelo.
:saveUpdate: se invoca cada vez que se actualizan los datos de un registro del modelo.


Asignar una función
-------------------

Es posible ejecutar una función personalizada cuando se lanza un evento del modelo. Para ello debemos
crear o modificar el archivo `Init.php <InitPHP>`__ y añadir en la función **init** una llamada al método
estático **attach** de la clase *EventManager*, donde el parámetro que se recibe es un puntero al
registro del modelo que ejecuta el evento.

Ejemplo para ejecutar una función al eliminar un producto.

.. code:: php

    EventManager::attach('Model:Producto:delete', function($model) {
        /*
          Aquí va las líneas de código que deseamos ejecutar.

          Nota:
          El parámetro $model contiene el producto que se ha eliminado
        */
    });


Eventos en personalizados
=========================

Podemos crear eventos nuevos, que serán usados por nuestro plugin u otros, declarando el evento
mediante el método estático **trigger** de la clase EventManager.

.. code:: php

    EventManager::trigger('NombreDelEvento', $parametrosOpcionales);
