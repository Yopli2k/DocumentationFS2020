.. highlight:: rst
.. title:: Facturascripts primeros pasos: Tu primer atributo
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Primeros pasos. Como crear atributos de productos en FacturaScripts 2020.
  :keywords: facturascripts, configurar, dar de alta, atributo, producto, talla, color
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Primer Atributo FacturaScripts 2020
  :lang: es

##################
Tu primer atributo
##################

FacturaScripts 2020 incorpora un sistema de atributos de productos que permite crear variantes de
un mismo producto de hasta una combinación de dos atributos distintos. Esto hace innecesario
estar creando multiples referencias para un mismo producto.

El concepto de atributo debe tratarse de manera abstracta y general. Un atributo puede ser
un color, una talla, un año o temporada, un modelo, etc. Cada atributo tiene asociada una
lista de valores que pueden tener los productos.

Algunos ejemplo:

    - Un mismo producto con 1 atributo: *temporada*
        - Un coche modelo 2018
        - Un coche modelo 2016

    - Un mismo producto con 2 atributos: *modelo* y *temporada*
        - Camiseta equipo fútbol modelo 1ra equipación de la temporada 2018
        - Camiseta equipo fútbol modelo 2da equipación de la temporada 2018

    - Varios productos sin atributos
        - Un coche
        - Una camiseta

Como puede verse en estos ejemplos, el atributo *modelo* tiene los valores *1ra equipación* y *2da equipación*,
mientras que el atributo *modelo* tiene los valores *2016* y *2018*.

Para crear, consultar o modificar los atributos debemos ir a la opción del menú
(:guilabel:`Almacén->Atributos`). Esta lista, si no se han instalado datos de prueba,
nos aparecerá vacía. Para crear un nuevo atributo debemos hacer clic en el botón de
insertar (botón con fondo verde y signo *+*) y rellenamos los campos del formulario.

Código: Se debe introducir un código para el atributo. Dicho identificador debe ser único, no se puede repetir.
Nombre: Se debe introducir un nombre o descripción para el atributo.

Al pulsar el botón de guardar, habremos creado el atributo. Ahora es necesario asignarle
los posibles valores que puede tener o usar.


Valores
=======

Estando consultando la ficha de un atributo podemos ver en la parte inferior la lista de los
posibles valores que ese atributo puede tener. Pulsando el botón *Nuevo* podemos informar un nuevo
valor indicando:

:Atributo: Código del atributo al que pertenece el valor que estamos creando. (Se rellena automáticamente).
:Valor: Nombre descriptivo del valor que estamos creando.

Al pulsar el botón de guardar, habremos creado un nuevo valor. Ahora podemos asignar este valor
a los productos que lo necesiten.
