.. title:: Development
.. highlight:: rst

.. title:: Facturascripts los controladores de acciones y procesos
.. meta::
   :description: Clase controladora de los procesos. Parte del modelo MVC.
   :keywords: facturascripts, documentacion, desarrollo, mvc, controlador, patron mvc


###########
Controlador
###########

Llamamos controlador a la clase que contiene el código necesario para responder a
las acciones que se solicitan desde la aplicación (usualmente acciones del usuario)
como visualizar un elemento, realizar un proceso, buscar la información, etc.
No es su responsabilidad ni manipular directamente datos, ni mostrar ningún tipo de
salida. En realidad es una capa intermedia que sirve de enlace  entre las vistas
(pantallas que se muestran al usuario) y los modelos de datos, respondiendo y aplicando
los mecanismos que puedan requerirse para implementar las necesidades de la aplicación.

Aunque se pueden encontrar diferentes implementaciones del patrón MVC, el flujo de
control que se sigue generalmente es el siguiente:

#. El usuario interactúa con la vista de alguna forma (pulsando un botón, sobre un enlace, etc).

#. El controlador recibe (por parte de la vista) la notificación de la acción solicitada por el usuario.

#. El controlador gestiona el evento que llega, frecuentemente a través de un gestor de eventos (handler) o callback.

#. El controlador accede al modelo, procesa los datos y en ocasiones actualizando los modelos de forma adecuada a la acción solicitada por el usuario.

#. El controlador delega a la vista la tarea de desplegar el resultado. La vista obtiene los datos que necesita para generar la interfaz apropiada para el usuario con los cambios solicitados.

#. La vista espera nuevas interacciones del usuario, comenzando el ciclo nuevamente ...


Declaración del controlador
===========================

A la hora de crear un controlador nuevo debemos seguir las siguientes normas:

- **Deben ubicarse en la carpeta Controller**.

- **Deben tener el mismo nombre que la clase**.

- **Deben heredar de *FacturaScripts/Core/Base/Controller*** o de un controlador extendido.

- Las propiedades y métodos **deben usar nomenclatura `lowerCamelCase <https://es.wikipedia.org/wiki/CamelCase>`_**

Ejemplo: *archivo MyNewPlugin.php*

.. code:: php

    <?php
    namespace FacturaScripts\Plugins\MyNewPlugin\Controller;

    use FacturaScripts\Core\Base\Controller;

    class MyNewController extends Controller
    {
        public function getPageData()
        {
            $pageData = parent::getPageData();
            $pageData['title'] = 'MyNewController';
            $pageData['menu'] = 'admin';
            $pageData['icon'] = 'fa-page';
            return $pageData;
        }

        public function privateCore(&$response)
        {
            parent::privateCore($response);
            $this->setTemplate('MyNewController');
        }
    }


Métodos obligatorios
====================

.. _getpagedata:

getPageData
-----------

Este método es ejecutado por el núcleo de *FacturaScripts* cada vez que se ejecuta el controlador,
al activar o actualizar el plugin. Debe devolver un array con los datos para la instalación
y configuración del controlador dentro del entorno de *Facturascripts*.
Como norma hay que llamar al *parent* del controlador para inicializar los valores por
defecto y asegurar un correcto funcionamiento de nuestro controlador.

Los valores que se pueden configurar son:

:title: Título de la vista
:icon: Icono de la fuente de texto *fontawesome*
:menu: Nombre del menú donde se introducirá el controlador
:submenu: (opcional) Segundo nivel del menú donde se introduciría el controlador
:orden: Podemos alterar el orden natural del sistema de menú para colocar nuestro controlador más arriba o abajo

.. code:: php

       public function getPageData()
       {
           $pagedata = parent::getPageData();
           $pagedata['title'] = 'Agentes';
           $pagedata['icon'] = 'fa-user-circle-o';
           $pagedata['menu'] = 'admin';
           return $pagedata;
       }


privateCore
-----------


publicCore
----------


Controladores Extendidos
========================
