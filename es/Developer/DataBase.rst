.. highlight:: rst
.. title:: Facturascripts, la clase DataBase y su uso
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Acceso y uso de la base de datos. Leer, modificar y borrar
  :keywords: facturascripts, documentacion, base de datos, postgresql, mysql


#############
Base de Datos
#############

La clase *DataBase* es la encargada de controlar la conexión con la base de datos y
todas las tareas relacionadas con la misma. Actualmente se soportan conexiones a los
motores `PostgreSql <https://www.postgresql.org>`_ y `MySQL <https://www.mysql.com>`_
(junto con homóloga `MariaDB <https://mariadb.org>`_).

Internamente se subdivide en varias clases que se engloban en función de su uso y necesidad,
pero que al estar incorporadas en el núcleo del *Facturascripts* son "transparentes" para el
desarrollador, no necesitando conocimientos avanzados para su uso.

Entre las funciones que gestiona, algunas de manera automática, está la gestión de conexión y
desconexión a los datos, la creación y verificación de las estructuras de las tablas,
la gestión ejecución de sentencias SQL, la gestión de transacciones y un conjunto de
utilidades para el tratamiento de la información.

.. warning::

  Aunque en los ejemplos usado más adelante se cree un nuevo objeto *DataBase*, a la hora de
  desarrollar no es necesario en la mayoría de casos ya que los modelos y controladores ya
  disponen de la propiedad *dataBase* que da acceso a la clase.


Gestión de la conexión
======================

conected
--------

Nos retorna un valor booleano que indica si estamos o no conectados a una base de datos.

connect
-------

Conecta con la base de datos configurada en el *config.php* de la aplicación, retornando
un valor booleano que indica si ha tenido éxito o no.

close
-----

Cierra la conexión actual retornando un valor booleano que indica si ha tenido éxito o no.

version
-------

Retorna la versión de la base de datos a la que estamos conectado.


Sentencias SQL
==============

Nos permite acceder y modificar los datos de la base de datos.

Ejemplos:

.. code:: php

    /// Obtener los primeros 50 clientes
    $dataBase = new DataBase();
    $sql = 'SELECT * FROM clientes';
    $data = $dataBase->selectLimit($sql, 50, 0);

    /// Actualizar el telefono del cliente 1
    $sql = 'UPDATE clientes SET telefono = ' . $dataBase->var2str('999-999999')
        . ' WHERE codcliente = ' . $dataBase->var2str('1');
    $dataBase->exec($sql);


select
------

Ejecuta una sentencia SQL de selección de datos y nos retorna un *array* con el resultado.
En caso de generar un error, porque la sentencia que se intenta ejecutar es errónea,
retorna un valor *false*.

selectLimit
-----------

Ejecuta una sentencia SQL de selección de datos pero con paginación y nos retorna
un *array* con los resultados. En caso de error nos retorna un *array* vacio.
El rango de datos que se solicita se indica mediante los parámetros numéricos:
- *limit*: Indica el número de registros que se desean.
- *offset*: Indica el número de desplazamiento o posición inicial desde donde se empieza a retornar los datos.

exec
----

Ejecuta una sentencia SQL de ejecución o acción (insert, update o delete) retornando
un valor booleano que indica si se ha realizado con éxito. Si no hay transacción abierta
en el momento de ejecutar la sentencia, el proceso se encarga de crear una, confirmarla o
cancelarla de acuerdo al resultado de la ejecución.

lastval
-------

Nos retorna el último identificador de registro que se ha creado al ejecutar un *Insert*.


Transacciones
=============

Permite saber y gestionar las transacciones para cambios masivos en los datos, retornando
un valor booleano indicando el estado o el éxito de la operación.

Ejemplos:

.. code:: php

    /// Ejemplo ejecución directa
    $dataBase = new DataBase();
    $dataBase->beginTransaction();
    try {
        $this->addRoleAccess($codrole, $pages);
        $dataBase->commit();
    } catch (\Exception $e) {
        $dataBase->rollback();
        $this->miniLog->notice($e->getMessage());
    }

    /// Ejemplo desde un Modelo
    $inTransaction = $this->dataBase->inTransaction();
    try {
        if ($inTransaction === false) {
            $this->dataBase->beginTransaction();
        }

        /// update master model
        if (!parent::delete()) {
            return false;
        }

        /// update detail model data
        $detail = new Detail();
        foreach ($lines as $row) {
            $detail->id = $row->id;
            if (!$detail->updateData($date, $row->import1, $row->import2)) {
                return false;
            }
        }

        /// save transaction
        if ($inTransaction === false) {
            $this->dataBase->commit();
        }
    } catch (\Exception $e) {
        $this->miniLog->error($e->getMessage());
        return false;
    } finally {
        if (!$inTransaction && $this->dataBase->inTransaction()) {
            $this->dataBase->rollback();
            return false;
        }
    }


inTransaction
-------------

Indica si existe una transacción abierta para la conexión actual.

beginTransaction
----------------

Comienza una transacción en la base de datos para la conexión actual.

commit
------

Finaliza la transacción actual **haciendo persistentes** los cambios realizados en los datos
desde el inicio de la transacción.

rollback
--------

Finaliza la transacción actual **deshaciendo** los cambios realizados desde el inicio de la transación.


Gestión de estructuras
======================

Nos dan información y tratamiento sobre la estructura de la base de datos.


tableExists
-----------

Retorna un valor *boleano* que indica si la tabla informada existe en la base de datos.


getTables
---------

Retorna un *array* con la lista de nombres de las tablas de la base de datos.


getColumns
----------

Retorna un *array* con la lista de campos de la tabla informada.


getConstraints
--------------

Retorna un *array* con la lista de constraints y sus propiedades de la tabla informada.


getIndexes
----------

Retorna un *array* con la lista de indices de la tabla informada.


Utilidades
==========

var2str
-------

Transforma un valor en un texto válido para ser usado en una sentencia SQL.


escapeString
------------

Formatea las comillas de una cadena de texto aplicando un escapado (\').


dateStyle
---------

Retorna el formato a utilizar para los datos fecha según la base de datos.


sql2Int
-------

Retorna el comando o función SQL para convertir una columna a numérico.
