.. highlight:: rst
.. title:: Facturascripts gestión de usuarios, grupos y permisos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: La gestión de usuario nos permite establecer permisos lectura, modificación y borrado.
  :keywords: facturascripts, documentacion, usuario, seguridad, permisos, niveles


###########################
Usuarios, Grupos y Permisos
###########################

El control de acceso en *Facturascripts* viene dado por la combinación de una lista de usuarios,
grupos que los agrupan y un conjunto de reglas que determinan los permisos que aplican
a cada una de las páginas para cada grupo. Es decir, un usuario tiene asignado uno o varios grupos,
y cada grupo tiene asignado las páginas y lo que puede hacer en cada una de ellas.

Además de indicar a que páginas el usuario tiene acceso y sus permisos, *Facturascripts* implementa
un sistema de **nivel por página** que nos permite indicar a cada una de las páginas que
nivel de seguridad se requiere para poder acceder a ella. Así de manera sencilla podemos tener
dentro de un mismo grupo de usuario, usuarios que accedan a una página y usuarios que no podrían acceder.

.. warning::

    Los usuarios sólo pueden acceder a las páginas asignadas a los grupos que pertenece.
    Los usuarios administradores pueden acceder a todas las páginas sin importar los grupos.


Usuarios
========

Podemos acceder a la lista de usuarios mediante la opción del menú :guilabel:`Administrador -> Usuarios`.
Haciendo click sobre un usuario de la lista podemos acceder a ver la información completa
o pulsaldo el botón de nuevo dar de alta un nuevo usuario.

.. image:: images/es/users-card.png
   :alt: Ficha de usuario

:Código: Es el identificador o "nick" del usuario.
:Contraseña: La contraseña de acceso.
:Administrador: Indica si el usuario es administrador de la aplicación.
:Activado: Indica si el usuario esta o no activo. Los usuarios desactivados no tienen acceso a la aplicación.
:Email: Correo electrónico para notificaciones.
:Nivel: Indica el nivel de permiso que tiene el usuario. Solo podrá operar con páginas con un nivel inferior o igual al indicado.
:Pág. de inicio: Página a la que se le redirecciona al realizar el login.
:Empresa: Empresa por defecto con la trabaja el usuario.
:Cód. de idioma: Idioma en el que se visualizarán las páginas.
:Últ. conexión: Fecha y hora del último login realizado.
:Última IP: Idendificación de red desde donde se ha realizado la conexión.

Dentro de la ficha del usuario podemos acceder a la lista de grupos a los que pertenece
pulsando sobre la pestaña lateral izquierda con el texto :guilabel:`Grupos`, donde
podemos añadir, modificar o eliminar a la lista.


Grupos
======

Un grupo nos permite crear un conjunto de usuario que compartirán permisos o reglas.
Un usuario puede pertenecer a distintos grupos. Podemos acceder a la lista de grupos
mediante la opción del menú :guilabel:`Administrador -> Usuarios`, en la pestaña :guilabel:`Grupos`.
Haciendo click sobre uno de los grupos de la lista podemos acceder a ver la información completa
o pulsaldo el botón de nuevo dar de alta un nuevo grupo.

.. image:: images/es/roles-card.png
   :alt: Ficha de grupos de usuario


Permisos
--------

Dentro de la ficha de cada grupo, podemos indicar los permisos o reglas que se aplicarán
a cada uno de los usuarios que pertenezcan al grupo. Los permisos son aplicados a cada
una de las páginas u opciones que tiene la aplicación y los usuarios sólo podrán ver las
páginas indicadas. Es decir, si no está la página en la lista de permisos, los usuarios
del grupo no tendrán la página en el menú de la aplicación (a menos que pertenezcan a
otro grupo que si la disponga)

.. image:: images/es/rules-card.png
   :alt: Ficha de permisos de usuario

:Permitir actualizar: Permite al usuario modificar los datos de la vista que está editando.
:Permitir eliminar: Permite al usuario eliminar registros de datos de la vista.

Estos permisos se complementan con el control de nivel del usuario. Si un usuario no tiene
el nivel necesario para ver una página, aunque esté en la lista de permisos, el usuario no
la tendrá disponible en el menú de la aplicación.
