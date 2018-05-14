.. title:: DataBaseWhere
.. highlight:: rst

.. title:: Facturascripts, la clase DataBaseWhere
.. meta::
   :description: Filtrado where de los datos. Uso de SQL, operadores y operaciones
   :keywords: facturascripts, documentacion, base de datos, where, filtro, condiciones


#############
Filtros Where
#############

A menudo al seleccionar, al modificar o al borrar información de la base de datos
necesitamos filtrar los registros con los que queremos trabajar. Este tipo de filtrado
en SQL se realiza mediante la cláusula *WHERE*. En *Facturascripts 2018* se ha implementado
una clase que nos facilita la creación de estas condiciones de filtrado de una manera
sencilla mediante un *array* de condiciones. De todo ello se encarga la clase **DataBaseWhere**.

Creación de Filtros
===================

Para crear un filtro *where* necesitaremos incluir en nuestra clase el uso del espacio
de nombre *FacturaScripts\Core\Base\DataBase\DataBaseWhere*, que nos dará acceso a la clase.
Luego simplemente crearemos un *array* con las condiciones de filtrado que necesitemos,
siendo cada una de las condiciones una instancia de la clase *DataBaseWhere*.

Al crear la instancia debemos informar de los parámetros:

-  **fields** : Nombre de campo o lista separada por '|' a los que se aplicará el valor.

-  **value** : Valor por el cual se filtra.

-  **operator** : (opcional)('=' por defecto) operador aritmético a aplicar. **['=', '<', '>', '<=', '>=', '<>', 'IN', 'IS', 'IS NOT', 'LIKE', 'REGEXP']**

-  **operation** : (opcional)('AND' por defecto) Indica el operador lógico a aplicar. **['AND', 'OR']**


Ejemplos:

.. code:: php

    /// where codagente = 'Agente01'
    $where = [new DataBaseWhere('codagente', 'Agente01')];

    /// where fecha >= '01-01-2018' and fecha <= '31-12-2018'
    $where = [
      new DataBaseWhere('fecha', '01-01-2018', '>='),
      new DataBaseWhere('fecha', '31-12-2018', '<='),
    ];

    /// where codcliente = '181432' and estado <> 'Pagado'
    $where = [];
    $where[] = new DataBaseWhere('codcliente', '181432');
    $where[] = new DataBaseWhere('estado', 'Pagado', '<>');

    /// where name = 'MyView' and nick is null
    $where = [
        new DataBaseWhere('name', 'MyView'),
        new DataBaseWhere('nick', 'null', 'IS')
    ];

    /// where codejercicio = '2018' and codcuentaesp in ('IVAREX','IVAREP','IVARRE')
    $where = [
        new DataBaseWhere('codejercicio', '2018'),
        new DataBaseWhere('codcuentaesp', 'IVAREX,IVAREP,IVARRE', 'IN')
    ];

Obtener sentencia WHERE
=======================

getSQLWhere
-----------

En el contexto del manejo de la base de datos, la mayoría de métodos esperan recibir
un array con las condiciones para el filtrado mediante *DataBaseWhere*, pero en ocasiones
necesitamos obtener la sentencia *where*. Para estos casos utilizamos este método **statico**.
Al llamarlo nos transformará el array de condiciones en una cadena de texto con
**' WHERE '** más el conjunto de condiciones o **vacía** si no se han informado condiciones.

.. code:: php

    /// where codagente = 'Agente01'
    $where = [new DataBaseWhere('codagente', 'Agente01')];
    $sqlWhere = DataBaseWhere::getSQLWhere($where);
