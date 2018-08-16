.. highlight:: rst
.. title:: Facturascripts, tablas en base datos relacionales
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Tablas de datos. Establece la estructura de una tabla en la base de datos
  :keywords: facturascripts, desarrollo, base de datos, tabla, mysql, postgresql


###############
Tablas de datos
###############

La definición de la estructura tablas de datos en la base de datos se realiza mediante archivos XML
incluidos en la carpeta *Table* y donde el nombre del archivo establece el nombre de la tabla.
Es importante para mantener la homogeinidad y evitar problemas posteriores, usar nombres
totalmente en minúsculas.

FacturaScripts se encarga de la revisión, creación y actualización de las mismas de manera:

    - Creando la tabla si no existe
    - Comprobando si tiene todas las columnas necesarias y son del tipo correcto
    - Comprobando las relaciones entre tablas


Columnas o campos
=================

Para crear la estructura usaremos la etiqueta **table** como grupo raíz del archivo xml
alternando etiquetas **column** para definir cada uno de los campos de la tabla.
Las columnas o campos se configura mediante las etiquetas:

:name: (obligatorio) Indica el nombre del campo. Recomendaciones:
        - Utilizaremos siempre todo en minúsculas.
        - Evitaremos nombre de campos cortos o abreviados, como id, clte, imp.
        - FS2018 se reserva el uso de campos como code, active, action.

:type: (obligatorio) Indica el tipo de dato que almacena la tabla.

        - **serial**: Entero autoincremental. Recomendado para las claves primarias.

        - **integer**: Entero sin decimales.

        - **double precision**: Número con decimales.

        - **boolean**: Valor lógico, true o false.

        - **character varying(*longitud*)**: Cadena alfanumérica de la longitud máxima indicada.

        - **text**: Texto de hasta 4000 caracteres. También conocido como *campo Memo*.

        - **date**: Almacena Fechas.

        - **time without time zone**: Almacena la parte horaria de una fecha.

:null: (opcional) Si la columna no admite valores null debemos indicar el valor NO.
        Si no se informa de esta etiqueta, se interpreta como YES.

:default: Permite indicar el valor por defecto a asignar en caso de no proporcionar uno.


.. code:: xml

        <?xml version="1.0" encoding="UTF-8"?>
        <table>
            <column>
                <name>idemployee</name>
                <type>serial</type>
                <null>NO</null>
                <default>nextval('employees_id_seq'::regclass)</default>
            </column>
            <column>
                <name>idcompany</name>
                <type>integer</type>
            </column>
            <column>
                <name>name</name>
                <type>character varying(100)</type>
                <null>NO</null>
            </column>
            <column>
                <name>note</name>
                <type>text</type>
            </column>
            <column>
                <name>registrationdate</name>
                <type>date</type>
                <null>NO</null>
            </column>
        </table>


Definición de Constraints
=========================

Es posible definir restricciones físicas dentro del motor de base de datos que nos
garanticen integridad de datos, tanto para valores duplicados como para integridad referencial
entre tablas. Esto se realiza mediante el uso de la etiqueta de grupo **constraint**
y las etiquetas **name** y **type**.

*Ejemplo de restricción de valores*

.. code:: xml

        <!-- No se puede repetir la combinación de codigo y empresa -->
        <constraint>
            <name>uniq_codigo_albaranesprov</name>
            <type>UNIQUE (codigo,idempresa)</type>
        </constraint>


*Ejemplo de relaciones entre tablas*

.. code:: xml

        <!-- No se puede eliminar la serie si tiene albaranes -->
        <!-- Si se cambia la serie se actualizan todos sus albaranes -->
        <constraint>
            <name>ca_albaranesprov_series</name>
            <type>FOREIGN KEY (codserie) REFERENCES series (codserie) ON DELETE RESTRICT ON UPDATE CASCADE</type>
        </constraint>
