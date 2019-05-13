.. highlight:: rst
.. title:: Facturascripts requisitos para instalación
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Software de facturación y contabilidad para pymes, fácil, libre
  :keywords: facturascripts, requisitos, instalar, facturacion, contabilidad
  :github_url: https://github.com/ArtexTrading/facturascripts-docs/blob/master/es/Overview.rst


########################
Requisitos e Instalación
########################

Requerimientos
==============

Para instalación y uso
    1. **MySql 5.5** o **Postgresql 9.0**.
    2. **Apache 2.X** u otro servidor web compatible con PHP.
    3. **PHP 7.0.8** o superior.

Además de la extensión PHP de conexión a la base de datos instalada se necesitan las extensiones:

    - bcmath
    - curl
    - gd
    - mbstring
    - openssl
    - simplexml
    - zip

Si se usa como servidor web Apache es necesario tener activado el módulo **mod_rewrite**.


Para desarrollo
    1. Requerimientos de uso
    2. Entorno de desarrollo PHP: NetBeens, PHPStorm o similar
    3. Composer y NPM: Para la instalación de requerimientos.


.. note::

   Para entornos con bases de datos MySql es necesario tener activado el motor **innodb**.
   Este Software no funciona sobre MyISAM.



Instalación
===========

Instalación desde archivo ZIP
-----------------------------

Acceder al sitio web de `FacturaScripts 2018 <https://www.facturascripts.com/descargar>`_,
descarga y descomprime el archivo en tu hosting o en la carpeta del servidor web de tu PC.
A continuación abre el navegador y escribe la url oportuna, es decir, el dominio
de tu web o http://localhost/facturascripts si lo has instalado en local,
y complete el formulario de instalación.

Instalación desde github
------------------------

Puede realizar la instalación descargando el archivo `ZIP <https://github.com/NeoRazorX/facturascripts/archive/master.zip>`_
directamente del proyecto en github y realizar una instalación desde archivo ZIP, descomprimiendo el archivo.
También puede realizar la instalación mediante consola. Para ello es necesario tener instalado
las herramientas git, composer y npm. Este tipo de instalación está más recomendada para desarrolladores.

.. code-block:: bash

        git clone https://github.com/NeoRazorX/facturascripts.git
        cd facturascripts
        composer install
        npm install


Configuración de Apache
-----------------------
Para el uso de urls amigables es necesario activar el módulo **mod_rewrite**, y configurar nuestro host
definido en el Apache con la directiva **AllowOverride All** (normalmente está definida como AllowOverride None).
Tras los cambios debemos reiniciar el servidor web.


Licencia
========

Licenciado bajo `licencia MIT <http://opensource.org/licenses/MIT>`_.

    Copyright (C) 2013-2018  Carlos Garcia Gomez  <carlos@facturascripts.com>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU Lesser General Public License as
    published by the Free Software Foundation, either version 3 of the
    License, or (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU Lesser General Public License for more details.

    You should have received a copy of the GNU Lesser General Public License
    along with this program. If not, see <http://www.gnu.org/licenses/>.


Contribuir al proyecto
======================

Este proyecto es software libre y todos son bienvenidos. Se puede colaborar de muchas maneras,
ayudando en el desarrollo, en las traducciones, en la documentación, en probar las nuevas versiones ... Consulta las páginas:

    - colaborar en `FacturaScripts <https://www.facturascripts.com/colabora>`__
    - lista de tareas en `Trello <https://trello.com/b/cMmIBn4j/facturascripts>`__
    - documentación en `FacturaScripts <https://www.facturascripts.com/doc>`__
    - chat en `Slack <https://facturascripts.slack.com/messages>`__


Directrices
-----------

1. Facturascripts utiliza PSR-1 y PSR-2.

2. Facturascripts está diseñado para utilizar las menos dependencias y mayor simplicidad posibles.
Esto significa que no todas las solicitudes de funciones serán aceptadas.

3. Facturascripts tiene un requisito de versión PHP mínimo de 7.0. Las solicitudes de PR deben respetar
este requerimiento. Se negará la integración con otros requerimientos de versión de PHP.

4. Todas las solicitudes de PR deben incluir pruebas unitarias para garantizar que el cambio funcione como
esperado y para evitar regresiones.


Issues (Problemas)
------------------

Cualquier duda, pregunta o error que encuentres lo puedes comentar en el chat: https://facturascripts.slack.com
o crear el tema correspondiente en https://github.com/NeoRazorX/facturascripts/issues


Pull Requests
-------------

Todas las colaboraciones son bien recibidas en FacturaScripts, pero por favor, lee lo siguiente antes:

Contenido
    Revisa que tu código respeta los estándares `PSR-1 <http://www.php-fig.org/psr/psr-1>`__ y `PSR-2 <http://www.php-fig.org/psr/psr-2>`__.

Documentación
    La documentación es algo que nos resulta imprescindible a todos para entender mejor como utilizar
    el código realizado por otros, o incluso para entender que hicimos nosotros mismos hace algún tiempo.


Escribiendo un Pull Request
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Título
    Idealmente, un Pull Request debe referirse a sólo un objetivo, así los cambios independendientes se pueden combinar con rapidez.
    Si quieres por ejemplo, corregir un error tipográfico y mejorar el rendimiento de un proceso, debes intentar en lo posible hacerlo
    en PR separados, así podemos incorporar uno rápidamente mientras el otro puede que se discuta.
    El objetivo es obtener un registro de cambios limpio y hacer que una reversión sea fácil.
    Si has encontrado un fallo/error tipográfico al escribir tus cambios que no están relacionados con tu trabajo, por favor haz otro
    Pull Request para ello. En algunos casos raros, te verás forzado a hacerlo en el mismo PR. En este tipo de situaciones,
    por favor añade un comentario en tu PR explicando porque debe ser así.

Registro de cambios
    Por cada PR, se debe proporcionar un registro de cambios.
    En las notas se pueden utilizar las siguientes secciones:

    #. ``Añadido`` para nuevas características.
    #. ``Cambiado`` para indicar cambios en funcionalidades existentes.
    #. ``Obsoleto`` para características que han pasado a estar obsoletas y que serán eliminadas.
    #. ``Eliminado`` para características obsoletas que han sido eliminadas.
    #. ``Corregido`` para cualquier corrección de errores.
    #. ``Seguridad`` para invitar a los usuarios a actualizar en caso de vulnerabilidades.

    Esto facilita que cualquier usuario entienda facilmente todos los cambios que le ofrece la actualización,
    y así tener más claro si le resulta urgente o no actualizar.


Colaborar en esta documentación
===============================

Esta documentación está realizada con documentos en formato RST (*ReStructured Text*) y compilados
con la utilidad Sphinx. Para la visualización se utiliza el tema Read the Docs.
Aunque actualmente está alojada como un proyecto privado de GitLab cualquier ayuda
o colaboración es bienvenida.

Si deseas colaborar o has encontrado alguna errata, por favor comunica via mail
con informatica@artextrading.com indicándonos tu cuenta de GitLab o datos de contacto
para que podamos añadirte al proyecto.
