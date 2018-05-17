.. highlight:: rst
.. title:: Facturascripts los controladores de acciones y procesos
.. meta::
   :description: Clase controladora de los procesos. Parte del modelo MVC.
   :keywords: facturascripts, documentacion, desarrollo, mvc, controlador, patron mvc
   :github_url: https://github.com/ArtexTrading/facturascripts-docs/blob/master/es/Controllers.rst


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

- Las propiedades y métodos **deben usar nomenclatura** `lowerCamelCase <https://es.wikipedia.org/wiki/CamelCase>`_

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


.. _getpagedata:

Método getPageData
==================

Este método **obligatorio** es ejecutado por el núcleo de *FacturaScripts* cada vez que se
ejecuta el controlador, al activar o actualizar el plugin. Debe devolver un array con
los datos para la instalación y configuración del controlador dentro del entorno de *Facturascripts*.
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


Acceso privado y público
========================

*FacturaScripts* no solamente sirve para que usted y sus empleados gestionen su empresa,
también permite que pueda ofrecer servicio a sus clientes. Esto significa que no sólo
personas autorizadas intenten acceder al controlador. Para gestionar las peticiones
el controlador dispone de dos métodos: *privateCore* y *publicCore*

publicCore
----------

Se ejecuta este método de entrada al controlador cuando no existe una identificación
autorizada por parte del usuario. Ver `Usuarios <Users>`_ para más información.
Este método es opcional, cuando estamos desarrollando un nuevo controlador, pues se muestra
la pantalla de *inicio de sesión* por defecto. Sólo debemos implementarlo cuando deseemos
implementar algo distinto.

privateCore
-----------

Se ejecuta este método de entrada al controlador cuando el usuario está correctamente
identificado y tiene permisos para la ejecución de dicho controlador. Como norma establecida
en *Facturascripts 2018* el método de trabajo dentro del *privateCore* es:

#. Recepción de los parámetros enviados por la vista, normalmente por post.
#. Ejecutar las tareas previas a la carga de datos. (método *execPreviousAction*)
#. Cargar los datos de los modelos. (método *loadData*)
#. Ejecutar las tareas posteriores a la carga de datos. (método *execAfterAction*)

.. warning::
    Los cambios realizados en los datos de un modelo tras la carga de datos no se verán reflejados en la vista

Esta manera de trabajar simplifica el entendimiento y seguimiento del código del controlador,
y aunque no todos los controladores se ajustan a este patrón se anima a mantenerlo de cara
a futuros mantenimientos del código.

Ejemplo:

.. code:: php

    public function privateCore(&$response, $user, $permissions)
    {
        parent::privateCore($response, $user, $permissions);

        $action = $this->request->get('action', '');
        if (!$this->execPreviousAction($action)) {
            return;
        }

        $this->loadData();
        $this->execAfterAction($action);
    }


El usuario y sus permisos
-------------------------

Podemos acceder a los datos del usuario identificado mediante la propiedad *user* y a sus
permisos con la propiedad *permissions*.

La propiedad *user* es una instancia del modelo User, permitiéndonos saber:

:nick: Nombre o alias del usuario
:email: Cuenta de correo para comunicaciones
:admin: Indica si la cuenta del usuario es de tipo administrador
:level: Nivel de seguridad hasta el cual tiene acceso
:homepage: Indica la página de inicio preferida por el usuario
:langcode: Indica el idioma seleccionado por el usuario

La propiedad *permissions* es una instancia de la clase ControllerPermissions con las propiedades:

:allowAccess: Indica si el usuario tiene permiso para leer/acceder al controlador
:allowDelete: Indica si el usuario tiene permiso para eliminar información desde el controlador
:allowUpdate: Indica si el usuario tiene permiso para modificar información desde el controlador

.. code:: php

    $user = $this->user->nick;
    $email = $this->user->email;
    if ($this->permissions->allowDelete) {
      [ ... ]
    }


Comunicación con la vista
=========================

Obtener parámetros
------------------

La comunicación entre la vista (o usuario) y el controlador se recoge mediante los métodos
implementados en la clase base de *Controller* y gracias al componente http-foundation de
Symfony.

:getFormData:  Retorna un array asociativo con la lista de parámetros enviados al controlador.
:request->get:  Recoge el valor del parámetro con el nombre indicado. Se puede establecer, mediante un segundo parámetro, un valor por defecto por si no está definido el parámetro solicitado.
:request->getClientIp:  Obtiene la IP del equipo que solicita la vista.

.. note::

    El parámetro **action** indica al controlador la tarea solicitada.


Uso de Cookies
--------------

Es posible leer y escribir cookies para la sesión actual del usuario. Para ello realizaremos
una llamada al método *cookies* del objeto *request* incluido en el controlador.
Para la escritura de una cookie es necesario declarar el uso del namespace *Symfony/Component/HttpFoundation/Cookie*.

:cookies->get: Obtiene el valor de la cookie con el nombre que indiquemos.
:cookies->set: Establece el valor de la cookie con el nombre que indiquemos. Podemos indicar el tiempo de expiración.

.. code:: php

    use Symfony\Component\HttpFoundation\Cookie;

    $expire = time() + 3600; /// +1 hora
    $this->response->headers->setCookie(new Cookie('MyCook', 'value', $expire));
    $this->request->cookies->get('MyCook');
