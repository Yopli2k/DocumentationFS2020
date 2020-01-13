.. highlight:: rst
.. title:: Cierre contable
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Contabilización del Cierre de ejercicio
  :keywords: FacturaScripts, documentacion, ejercicio, cierre, cierre contable, asientos
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Cierre Contable FacturaScripts
  :lang: es


###############
Cierre Contable
###############

Este proceso, que se debe realizar al finalizar cada ejercicio, es el encargado de
generar el asiento de regularización, el de cierre de ejercicio y el de apertura del
nuevo ejercicio.

El asiento de regularización, es el encargado de traspasar los saldos de las subcuentas
de compras (*grupo 6*) y de ventas (*grupo 7*) a la subcuenta de pérdidas y ganancias (grupo *129*).

El asiento de cierre de ejercicio, se encarga de "anular" los saldos de las cuentas en la
fecha de final del ejercicio dejando todo el ejercicio a cero.

El asiento de apertura, recoge los saldos que había antes del asiento de cierre y los
añade como primer asiento del ejercicio.

Todo este proceso se realiza de manera automatizada, facilitando la labor del usuario.

.. important::
    Siempre antes de crear un nuevo asiento durante el cierre se procede a eliminar
    cualquier asiento de regularización, cierre y apertura ya existente.


Cómo cerrar
===========

Para realizar el cierre debemos primero ir a la ficha del ejercicio que deseamos cerrar.
Vamos a la opción del menú (:guilabel:`Contabilidad->Ejercicios`) para ver la lista de
ejercicios disponibles. Una vez localizado el ejercicio a cerrar hacemos click sobre la
fila para acceder a sus datos.

En el pie de la ficha con los datos, en la parte inferior, vemos un apartado con el título
*Acciones especiales* donde podemos ver un botón de color rojo con el título **Cerrar ejercicio**.

Si hacemos click sobre el botón nos aparecerá una nueva ventana donde se nos pregunta sobre
el diario donde incluir los asientos de cierre (regularización y cierre) y apertura, y sobre
si desemos copiar el plan de cuentas del ejercicio que estamos cerrando en el nuevo ejercicio.

Para elegir el diario, si deseamos incluir los asiento en alguno, simplemente debemos elegir uno
de los disponibles de la lista que se despliega. De lo contrario dejamos la lista son seleccionar.

Para que no se copie el plan de cuentas desmarcamos la casilla que el título *Copiar plan de cuentas*.
Indicar que este proceso copia sólo las subcuentas con saldo al final del ejercicio.

Para lanzar el proceso pulsaremos sobre el botón *Aceptar*. Por el contrario si deseamos regresar
bastará con pulsar sobre el botón *Cancelar*.


Cuenta de PYG
-------------

Antes de comenzar con el proceso de regularización se realiza una búsqueda entre las subcuentas para
localizar la subcuenta marcada como *pérdidas y ganancias*. En caso de no encontrarse el proceso se
cancelará mostrando el error *Subcuenta de Pérdidas y Ganancias no encontrada*.

Para indicar a FacturaScripts cual es la subcuenta a utilizar, se utiliza el código cuenta especial de
cuenta **PYG**. Esto se puede realizar marcando el grupo/cuenta o la subcuenta que desemos con dicho código
especial. Si se marca un grupo/cuenta se utilizará la primera subcuenta perteneciente al grupo/cuenta.

Para selecionar el grupo/cuenta o subcuenta debemos ir a la opción del menú
(:guilabel:`Contabilidad->Cuentas contables`) donde selecionaremos la pestaña **cuenta** o **subcuenta**.
Localizamos el registro, hacemos click sobre la fila para editarlo y en el campo *Cuenta especial* seleccionamos
*Pérdidas y ganancias*. Haremos click sobre el botón de *Guardar* para confirmar el cambio.


Nuevo ejercicio
---------------

El proceso además de realizar los procesos comentados se dará de alta, en caso de no existir, el nuevo
ejercicio utilizando el mismo periodo fechas pero dentro del siguiente año natural y calculando un
código automático.

En caso de desear tener una codificación no automática para los ejercicios es necesario dar de alta
el nuevo ejercicio antes de ejecutar el cierre. Para ello debemos ir a la opción del menú
(:guilabel:`Contabilidad->Ejercicios`) y pulsar sobre el botón verde con el título *+*. Rellenamos
los datos para el nuevo ejercicio asegurándonos de que el periodo de fechas es consecutivo al periodo
del ejercicio que deseamos cerrar.


Abrir un ejercicio cerrado
==========================

Si deseamos reabrir un ejercicio debemos ir a la ficha del **ejercicio cerrado**.
Debemos ir a la opción del menú (:guilabel:`Contabilidad->Ejercicios`) para ver la lista de
ejercicios disponibles. Una vez localizado el ejercicio cerrado, podemos comprobar el estado
en la columna *Estado* así con el color de la fila, hacemos click sobre la fila para acceder
a sus datos.

En el pie de la ficha con los datos, en la parte inferior, vemos un apartado con el título
*Acciones especiales* donde podemos ver un botón de color amarillo con el título **Abrir ejercicio**.

Si hacemos click sobre el botón nos aparecerá una nueva ventana donde se nos pregunta sobre
que asientos deseamos eliminar, el asiento de apertura y el de cierre. Combinando las distintas
opciones, marcando una o las dos opciones nos permite:

:Eliminar sólo el asiento de apertura:
    Si marcamos sólo la opción de eliminar la apertura el ejercicio continuará cerrado, pero
    eliminaremos los saldos iniciales del ejercicio nuevo.

:Eliminar sólo el asiento de cierre:
    Si marcamos sólo eliminar el cierre, se eliminará el asiento de regularización y cierre del
    ejercicio seleccionado dejando los saldos iniciales en el ejercicio nuevo. Esto posibilita
    listar balances con saldos de apertura "teóricos" en el nuevo ejercicio mientras se "termina"
    de cerrar completamente las subcuentas del ejercicio terminado. Se restaurará el estado del
    ejercicio a *Abierto*.

:Eliminar los dos asientos:
    Si marcamos eliminar ambos procesos, se eliminará completamente la apertura del nuevo ejercicio
    y la regularización y cierre del ejercicio seleccionado. Se restaurará el estado del ejercicio a
    *Abierto*.
