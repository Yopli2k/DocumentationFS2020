.. highlight:: rst
.. title:: Facturascripts primeros pasos: Tu primer producto
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Primeros pasos. Como crear productos y variantes en FacturaScripts 2020.
  :keywords: facturascripts, configurar, dar de alta, producto, variante, stock
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Primer Producto FacturaScripts 2020
  :lang: es

##################
Tu primer producto
##################

Para ver y administar los productos vamos a la opción de menú (:guilabel:`Almacén->Artículos`).
Si acabamos de instalar sin datos de prueba, el listado de productos debería estar vacío.
Para crear un nuevo producto hacer click en el botón de insertar (botón con fondo verde y signo *+*)
haciendo aparecer el formulario o ficha producto.

:Referencia: Identificador interno del producto. Este campo es obligatorio.
:Fabricante: Indica quién fabrica el producto. Se debe elegir de la lista de fabricantes creados previamente en (:guilabel:`Almacén->Fabricantes`).
:Familia: Indica la Familia/Subfamilia del producto. Se debe elegir de la lista de familias creadas previamente en (:guilabel:`Almacén->Familias`).
:Impuesto: Indica el porcentaje de impuesto que se aplica al producto. Se debe elegir de la lista de impuestos creados previamente (:guilabel:`Contabilidad->Impuestos->Impuestos`).
:Descripción: Una descripción completa del artículo. Permite tener más de una línea.
:Sin stock: Establece el producto como sin control de stock. Esto es útil para productos de tipo servicio y similares donde no existe físicamente el producto.
:Se compra: Indica que el producto debe listarse en la introducción de documentos de compra.
:Se vende: Indica que el producto debe listarse en la introducción de documentos de venta.
:Público: Tendrán acceso a la ficha del producto todos los usuarios de Facturascripts.
:Bloqueado: Bloquea el producto para que no se pueda usar en nuevos documentos de compra o venta.
:Vta sin stock: *(Permitir Venta Sin Stock)* Permitimos que se pueda facturar el producto aún cuando el stock físico se encuentre a 0 (tendremos stocks negativos).

Además de los campos anteriores, de manera opcional, podemos indicar unas cuentas contables
para compra, venta e impuestos para el producto. Si no se informa se usarán las cuentas establecidas
en niveles superiores según el órden Artículo, Familia, Empresa.

.. note::
    Para el plan contable español se usarían las cuentas:
        - Para las compras: Cuenta del grupo 6.
        - Para las ventas: Cuenta del grupo 7.
        - Para las retenciones: Cuenta del grupo 4.


Variantes
=========

En FacturaScripts 2020 los productos son *plantillas* generales de los productos que realmente
compramos o vendemos. Lo que realmente usamos en los documentos de compra y venta son las variantes.
Esto quiere decir que **todo producto debe tener al menos una variante**. Las variantes nos
permiten tener, en caso de necesitarlo, distintas versiones de un mismo producto según carasterísticas
que varian. Lo más común es la talla o el color, pero podría ser también la temporada,
la calidad, el material de fabricación, etc.

Para añadir variantes al producto usaremos, situados en la pestaña *Variantes* dentro del formulario
de edición del producto, el botón de insertar (botón con fondo verde y signo *+*) y rellenaremos
los campos del formulario.

:Atributo 1 y 2: Indicaremos las caracteristicas propias del producto. Se debe elegir de la lista de atributos creados previamente en (:guilabel:`Almacén->Atributos`).
:Código Barras: Indicamos el código de barras, código EAN o cualquier otro formato.
:Precio: Es el precio de venta base para esta variante del producto.
:Coste: *(Precio de Coste)* Es el precio de coste para esta variante del producto.


Stock
=====

Desde esta pestaña del formulario del producto, podemos consultar y modificar las cantidades de stock
de cada una de las variantes o añadir una cantidad inicial mediante el botón *Nuevo*.

Los campos a rellenar son:

:Referencia: Indica la variante del producto al que pertenece las cantidades mostradas.
:Almacén: Indica a que almacén pertenece las cantidades mostradas. Esto también establece la empresa. Se debe elegir de la lista de almacenes creados previamente en (:guilabel:`Almacén->Almacenes`).
:Cantidad: Stock actual del producto.
:Mín y Máx: *(Stock Mínimo y Stock Máximo)* Stock que deseamos tener como mínimo y máximo en el almacén seleccionado.


Junto con los campos editables se informan varios valores que nos proporcionan información adicional del estado del stock.

:Reservado: Cantidad pendiente de servir de los pedidos de venta realizados.
:Recepción: *(Pendiente de recepción)* Cantidad pendiente de recibir de los pedidos de compra realizados.
:Disponible: Stock que "realmente" se puede vender una vez quitado el stock reservado por los pedidos de venta y que aún no han sido servidos.
