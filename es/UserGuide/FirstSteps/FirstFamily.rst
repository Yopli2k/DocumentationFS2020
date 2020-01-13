.. highlight:: rst
.. title:: Facturascripts primeros pasos: Tu primera familia
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Primeros pasos. Como crear familias y subfamilias de productos en FacturaScripts 2020.
  :keywords: facturascripts, configurar, dar de alta, familia, subfamilia, producto
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Primera Familia FacturaScripts 2020
  :lang: es

##################
Tu primera familia
##################

En FacturaScripts 2020 se continua con el sistema clásico de familia y subfamilia en forma
de árbol, es decir un "padre" (*familia*) tiene varios "hijos" (*subfamilias*). Estas subfamilias a su
vez pueden ser "padre" de otros "hijos".

Para la creación de una familia nos vamos a la opción del menú (:guilabel:`Almacén->Familias`).
Si no se han instalado datos de prueba, la primera vez nos aparecerá la lista vacía. Para crear una nueva familia
debemos hacer clic en el botón de insertar (botón con fondo verde y signo *+*) y rellenamos los campos del formulario.

:Código: Será el identificador de la familia o subfamilia.
:Descripción: Descripción de la familia o subfamilia para que el usuario la reconozca en pantalla y listados.
:Padre: Nos permite indicar si la familia o subfamilia está agrupada en otro nivel superior.

Además de los campos anteriores, de manera opcional, podemos indicar unas cuentas contables
para compra, venta e impuestos para la familia o subfamilia. Si no se informa se usarán las cuentas establecidas
en según el órden: Artículo, Familia, Empresa.

.. note::
    Para el plan contable español se usarían las cuentas:
        - Para las compras: Cuenta del grupo 6.
        - Para las ventas: Cuenta del grupo 7.
        - Para las retenciones: Cuenta del grupo 4.
