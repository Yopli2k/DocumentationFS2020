.. highlight:: rst
.. title:: Facturascripts gestión de usuarios, permisos y seguridad
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: La gestión de usuario nos permite establecer permisos lectura, modificación y borrado.
  :keywords: facturascripts, documentacion, usuario, seguridad, permisos, niveles
  :github_url: https://github.com/ArtexTrading/facturascripts-docs/blob/master/es/Users.rst


###################
Usuarios y permisos
###################

El control de acceso en *Facturascripts* viene dado por la combinación de una lista de usuarios,
roles o grupos que los agrupan y un conjunto de reglas que determinan los permisos que aplican
a cada una de las páginas para cada rol. Es decir, un usuario tiene asignado uno o varios roles,
y cada rol tiene asignado las páginas y lo que puede hacer en cada una de ellas.

Además de indicar a que páginas el usuario tiene acceso y sus permisos, *Facturascripts* implementa
un sistema de nivel por página que nos permite indicar a cada una de las páginas que
nivel de seguridad se requiere para poder acceder a ella. Así de manera sencilla podemos tener
dentro de un mismo grupo de usuario o rol, usuarios que accedan a una página y usuarios
que no podrían acceder.

.. warning::

    Los usuarios sólo pueden acceder a las páginas asignadas a los roles que pertenece.
    Los usuarios administradores pueden acceder a todas las páginas sin importar los roles.


Usuarios
========

Podemos acceder a la lista de usuarios mediante la opción del menú :guilabel:`Administrador -> Usuarios`.
Haciendo click sobre un usuario de la lista podemos acceder a ver la información completa
o pulsaldo el botón de nuevo dar de alta un nuevo usuario.

.. image:: ../images/es/users-card.png
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

Dentro de la ficha del usuario podemos acceder a la lista de roles o grupos a los que pertenece
pulsando sobre la pestaña lateral izquierda con el texto :guilabel:`Roles`, donde
podemos añadir, modificar o eliminar a la lista.


Roles
=====

.. note::

    Este tema está pendiente. Por favor vuelve pasado un tiempo.


Reglas
------

.. note::

    Este tema está pendiente. Por favor vuelve pasado un tiempo.
