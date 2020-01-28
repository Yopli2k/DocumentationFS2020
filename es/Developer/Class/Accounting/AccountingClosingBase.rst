.. highlight:: rst
.. title:: Facturascripts Clase Base para procesos de Cierre Contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Clase Base para procesos de Cierre Contable.
  :keywords: facturascripts, cierre contable, AccountingClosingBase
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Clase Base
  :lang: es


#####################
AccountingClosingBase
#####################

Todo el proceso de cerrar un ejercicio y abrir uno nuevo se realiza en tres pasos:
    - Regularización: donde se saldan las subcuentas de compras y ventas
    - Cierre contable: donde se saldan el conjunto de subcuentas
    - Apertura: donde se traspasan los saldos del cierre al nuevo ejercicio

Estos procesos tienen "rutinas parecidas" en muchos de sus pasos que se han unificado
en esta clase base, de donde heredan cada uno de los procesos de cierre.

Así, existen dos métodos públicos, **exec** y **delete** que crean y eliminan los asientos
y un conjunto de métodos protected que permiten personalizar el proceso general para cada
uno de los pasos. Ambos métodos deben recibir un objeto del modelo *Ejercicio* como
indicador donde se realizará el proceso de cierre contable.

La clase dispone de la propiedad **exercise** con los datos del ejercicio que se
está procesando.


Métodos GET
===========

Estos métodos son llamados para obtener información sobre el proceso que se está ejecutando.

:getBalance: Obtiene un array (que contiene otro array) con los saldos de las subcuentas por cada canal.
             La estructura del array es:

             [canal]
             [ 'id' => id subcuenta, 'code' => subcuenta, 'debit' => debe, 'credit' => haber ]

:getConcept: (Abstracta) Obtiene el concepto para el asiento y cada una de sus líneas.

:getDate: (Abstracta) Obtiene la fecha para el asiento.

:getOperation: (Abstracta) Obtiene el identificador para el tipo de operación (tipo de asiento).

      - 'A': Asiento de apertura.

      - 'R': Asiento de regularización.

      - 'C': Asiento de cierre de ejercicio.

:getOperationFilter: Obtiene el tipo de operación para el filtrado de cuentas al obtener el balance.

:getSubAccountsFilter: (Abstracta) Obtiene el filtro de las subcuentas a calcular en la obtención del balance.

:getSQL: Obtiene el SQL para calcular los saldos de las cuentas.

:getSQLFields:
    Obtiene la lista de campos o columnas de datos del método **getBalance**. Es llamado por el método **getSQL**.
    Los campos por defecto que se obtienen son:
    - channel: (agrupado por) es un valor numérico que identifica el canal.
    - id: (agrupado por) es el identificador numérico (PK) de la subcuenta.
    - code: (agrupado por) es el código de la subcuenta.
    - debit: la suma total de los importes en el debe de la subcuenta.
    - credit: la suma total de los importes en el haber de la subcuenta.


Métodos SET
===========

Estos métodos se utilizan para establecer datos generales o por defecto.

:newAccountEntry: Crea un nuevo asiento para el canal y el diario informado.
:setData: Asigna los valores a la cabecera del asiento.
:setDataLine: Asigna los valores a la línea del asiento que se está procesando.


Métodos SAVE
============

:saveLines: Graba en el asiento la línea con el saldo de la subcuenta.
:saveBalanceLine: Graba en el asiento la línea de cuadre de saldos del asiento.
:deleteAccountEntry: Elimina el asiento y todas sus líneas. Se debe indicar el tipo de operación que identifica el asiento.
