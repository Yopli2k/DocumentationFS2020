.. title:: ModelView
.. highlight:: rst

#########################
Modelos de sólo visionado
#########################

.. note::

  Debido a que este modelo es **sólo para la visualización** de datos tiene una estructura básica,
  no usando la estructura completa de los modelos de datos estándar.

Para aquellos casos en los que deseamos mostrar información interelacionada almacenada en
distintas tablas de la base de datos podemos usar este tipo de modelo. Su implementación
es muy sencilla y rápida, necesitando sólo unos pocos métodos para su correcto funcionamiento.

Cómo usar el modelo
===================

Para crear un modelo de sólo visualización debemos crearnos una clase que extienda la clase
*Base/ModelView* en vez de la clase de los modelos de datos, implementándose automáticamente
los métodos necesarios por la vista para la obtención de los datos como *count* y *all*.
Para que esta obtención automática de datos funcione es necesario implementar los métodos
*getTables*, *getFields* y *getSQLFrom* que informan la de estructura que queremos obtener.
(Se detallan en las siguientes secciones)

La gestión de propiedades del modelo (los "campos" que se quieren visualizar) se realiza
mediante los `métodos mágicos <http://php.net/manual/es/language.oop5.magic.php>`_ de PHP por lo que no requieren de declaración
previa, en cargándose del proceso la clase *ModelView*. Sólo si deseamos tener campos calculados debemos
sobrescribir los métodos *clear* y *loadFromData* donde asignaremos sus valores.

.. code:: php

    protected function clear()
    {
        parent::clear();

        $this->cuotaiva = 0.00;
        $this->cuotarecargo = 0.00;
        $this->total = 0.00;
    }

    protected function loadFromData($data)
    {
        parent::loadFromData($data);

        $this->cuotaiva = $this->baseimponible * ($this->iva / 100.00);
        $this->cuotarecargo = $this->baseimponible * ($this->recargo / 100.00);
        $this->total = $this->baseimponible + $this->cuotaiva + $this->cuotarecargo;
    }


Métodos obligatorios
====================

getTables
---------

Para el control de existencia y creación automática de los modelos es necesario informar
de la lista de tablas que vamos a utilizar en la obtención de los datos. Lo haremos
retornando un array con la **lista de tablas**. *(No la clase modelo que referencia la tabla)*

.. code:: php

    protected function getTables(): array
    {
        return [
            'asientos',
            'partidas',
            'subcuentas'
        ];
    }


getFields
---------

Es el método encargado de retornar un array asociativo con la lista de campos y su "alias"
que deseamos visualizar.

.. code:: php

    protected function getFields(): array
    {
        return [
            'codejercicio' => 'asientos.codejercicio',
            'codcuentaesp' => 'subcuentas.codcuentaesp',
            'descripcion' => 'cuentasesp.descripcion',
            'codimpuesto' => 'subcuentas.codimpuesto',
            'iva' => 'partidas.iva',
            'recargo' => 'partidas.recargo',
            'baseimponible' => 'SUM(partidas.baseimponible)'
        ];
    }


getSQLFrom
----------

El detalle de las tablas a utilizar se realiza mediante este método que nos retorna
una cadena de texto con la cláusula *FROM* a utilizar en la sentencia SQL.

.. code:: php

    protected function getSQLFrom(): string
    {
        return 'asientos'
            . ' INNER JOIN partidas ON partidas.idasiento = asientos.idasiento'
            . ' INNER JOIN subcuentas ON subcuentas.idsubcuenta = partidas.idsubcuenta'
            . ' AND subcuentas.codimpuesto IS NOT NULL'
            . ' AND subcuentas.codcuentaesp IS NOT NULL'
            . ' LEFT JOIN cuentasesp ON cuentasesp.codcuentaesp = subcuentas.codcuentaesp';
    }


Métodos opcionales
==================

getGroupBy
----------

Para los casos que deseemos agrupar información para obtener totales o datos estadísticos
podemos definir las cláusulas *group by* y *having* de la sentencia SQL mediante la declaración
de este método. Debemos devolver una cadena de texto con el valor a aplicar.

.. code:: php

    protected function getGroupBy(): string
    {
        return 'GROUP BY asientos.codejercicio, subcuentas.codcuentaesp,'
                      . 'cuentasesp.descripcion, subcuentas.codimpuesto,'
                      . 'partidas.iva, partidas.recargo';
    }
