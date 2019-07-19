.. highlight:: rst
.. title:: Archivo Cron.php
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Automatización de tareas
  :keywords: facturascripts, configurar, automatizar, tareas, cron
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Archivo Cron.php
  :lang: es

################
Archivo Cron.php
################

*FacturaScripts* utiliza de un proceso automatizado denominado **cron** para ciertas tareas
como generar los documentos contables (libro diario, etc), acelerar procesos, como la sincronización
con WooCommerce o PrestaShop, etc. También es posible añadir procesos específicos de plugins
(sólo si están activos) a la lista de tareas automáticas.

Así que si necesita ejecutar un proceso de forma periódica, el mejor lugar es el cron de su plugin.

Para añadir estas tareas, debemos crear o incluir en el raíz de nuestro plugin un archivo denominado
*cron.php* que contendrá la clase **Cron**. Esta clase debe heredar de la clase base **CronClass**,
e implementaremos el método público **run**.

Ejemplo.

.. code:: php

    <?php
    namespace FacturaScripts\Plugins\MyNewPlugin;

    use FacturaScripts\Core\Base\CronClass;

    class Cron extends CronClass
    {

        public function run()
        {
            /*
              Aquí pondremos las líneas de código a ejecutar
            */
        }
    }


Ejecutar manualmente
====================

Existen dos maneras de ejecutar manualmente los procesos definidos en el cron de su plugin.


Desde el navegador
------------------

Simplemente añadir a la url de su instalación la ruta **/cron**. Por ejemplo: https://localhost/facturascripts/cron


Desde una terminal
------------------

Llamar al archivo index.php añadiendo el parámetro -cron en la llamada.

.. code-block:: bash

    cd /ruta/instalacion/facturascripts
    php index.php -cron


Ejecutar automáticamente
========================

Para programar las ejecuciones de manera automática debemos incluir la llamada al a la tarea dentro del cron
del sistema o host donde tenemos la instalación de *FacturaScripts*. Debemos utilizar el método *Desde una terminal*
descrito anteriormente.


Control de ejecución
--------------------
La manera de establecer si es necesario ejecutar la tarea o no, es mediante el método **isTimeForJob** que determina
si ha pasado el tiempo necesario desde la última ejecución.

Una vez ejecutadas las operaciones de la tarea es necesario llamar al método **jobDone** para indicarle a
*FacturaScripts* que se ha terminado correctamente la tarea, y establecer la próxima ejecución.

Ejemplo para ejecución cada 6 horas.

.. code:: php

    class Cron extends CronClass
    {

        public function run()
        {
            if ($this->isTimeForJob('my-job-name', '6 hours')) {
                /*
                  Aquí pondremos las líneas de código a ejecutar
                */

                $this->jobDone('my-job-name');
            }
        }
    }
