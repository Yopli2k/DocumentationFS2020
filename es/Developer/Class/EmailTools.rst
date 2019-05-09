.. highlight:: rst
.. title:: Facturascripts, Clase EmailTools, envío de mails
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Envío de mails. Plantillas de mails
  :keywords: facturascripts, documentacion, mail, plantilla, template, envíar mails
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: EmailTools FacturaScripts
  :lang: es


##########
EmailTools
##########

Esta clase simplifica y automatiza el envío de mails. Nos permite enviar comunicaciones electrónicas
totalmente personalizables mediante una lista de valores y usando una plantilla de Twig para dar
formato visual al contenido del mail.

.. important::

    Para el correcto funcionamiento debemos primero establecer la configuración del servidor y la cuenta
    de correo que usaremos para los envíos, y lo hacemos en la opción del menú
    (:guilabel:`Administrador->Panel de Control->Preferencias de aplicación`) en la pestaña *Email*.


Sistema de plantillas
=====================

Para el diseño visual del mail se utiliza una plantilla Twig. *FacturaScripts* dispone de una plantilla
base *BasicTemplate.html.twig* pero podemos crear nuestras propias plantillas. Las plantillas personalizadas
deben situarse dentro de la carpeta *View* de nuestro plugin en una nueva carpeta que denominaremos **Email**.
El nombre del archivo debe llevar las extensiones **.html.twig**.

Las plantillas pueden llevar variables o macros que son substituidas por su valor en el momento de renderizar
la plantilla. Estas variables deben estar definidas entre doble corchete *[[xxx]]*.

Ejemplo de plantilla con variables: *title*, *company*, *body*, *footer*

.. code:: html

    <!DOCTYPE html>
    <html>
        <head>
            <title>[[title]]</title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
        </head>
        <body>
            <h3 class="text-center">[[company]]</h3>
            <div class="container">[[body]]</div>
            <p class="text-center">[[footer]]</p>
        </body>
    </html>

Al usar el componente Twig las plantillas también pueden utilizar la programación propias de este sistema,
el sistema de traducción integrado en *FacturaScripts* y así como una lista de objetos personalizados
informados por el desarrollador en la llamada (ver más adelante).


.. code:: html

    <body>
        <h3 class="text-center">[[company]]</h3>
        <p>{{ i18n.trans('my-company-info-header') }}</p>
        <div class="container">[[body]]</div>
        <p class="text-center">[[footer]]</p>
        <p>{{ i18n.trans('my-company-info-footer') }}</p>
    </body>


Cómo mandar un mail
===================

Existen dos métodos para crear y mandar un mail:
    - el método estático **sendMail** que realiza todo el proceso de manera automática en base a los parámetros informados

    - crear una instancia de EmailTools, configurarla y finalmente mandarlo con el método público *send*.


sendMail
--------

Este método ayuda a envíar un correo de manera totalmente automática simplemente informando el
parámetro *data*, que es un array que contiene la configuración a utilizar en base a las claves y valores:

:subject: (string) Asunto o título del correo. **(requerido)**
:body: (string) Texto que conforma el mensaje. Puede ser código html. **(requerido si no se informa una plantilla)**
:email: (string) Lista de cuentas de correo destinatarias, separada por comas. **(requerido)**
:email-cc: (string) Lista de cuentas de correo donde se mandará una copia de cortesía del correo.
:email-bcc: (string) Lista de cuentas de correo donde se mandará una copia de manera oculta del correo.
:files: (string|array) Ruta y nombre de un archivo o lista de archivos que se adjuntarán al correo.
:template: (string) Plantilla Twig con la que diseñar el correo.
:template-data: (array) Lista de valores a usar en la plantilla. Ejemplo: [ 'mydate' => '01/01/2019', 'myvalue' => 'custom value' ].
:template-object: (array) Lista de objetos que se "pasarán" a la plantilla. Estos objetos estarán disponibles en la plantilla Twig. Ejemplo: [ 'fsc' => $this, 'company' => $company ].

send *(manualmente)*
-------------------

Este método nos permite realizar el envío de manera manual, configurando nosotros cada uno de
los pasos en la creación y envío del correo. Los pasos a seguir son:

1. Crear un objeto EmailTools
2. Obtener un objeto mail (PHPMailer)
3. Configurar el mail
    3.1 Establecer el asunto del mail
    3.2 Asignar la lista de correos a donde enviar el mail
    3.3 Asignar, si lo hay, los archivos adjuntos
    3.4 Generar el mensaje del correo en base a una plantilla. Si no se indica plantilla se usa la estandar de *FacturaScripts.
4. Enviar el mail
5. Si hay archivos adjuntos, eliminar los archivos temporales

Ejemplo:

.. code:: php

     /// Prepare email object
     $emailTools = new EmailTools();
     $mail = $emailTools->newMail();
     $mail->Subject = 'This is a example of manual mail';

     /// Set email list
     $emailTools->addEmails($mail, 'myaccount@my-server.com', 'onecopy@to-you.com', '');

     /// Set attachment files
     $emailTools->addAttachment($mail, 'my-file.doc');

     /// Load template and set data.
     $body = $emailTools->getTemplateHtml(['company' => 'My Company']);
     $mail->msgHTML($body);

     /// Send Email
     $emailTools->send($mail);

     /// Remove upload files
     if (!empty('my-file.doc') && file_exists(FS_FOLDER . '/MyFiles/' . 'my-file.doc'])) {
         unlink(FS_FOLDER . '/MyFiles/' . 'my-file.doc']);
     }


Métodos disponibles
===================

addAttachment
-------------

Adjunta un archivo o una lista de archivos al correo informado. Los parámetros son:

:mail: (PHPMailer) Puntero al objeto mail encargado del envío.
:files: (string|array) Nombre del archivo o lista de nombres de archivos.


addEmails
---------

Añade una dirección de correo o una lista de direcciones (destinatarios) al mail informado.
Las listas de direcciones son una relacion de direcciones separadas por una coma entre ellas.
Los parámetros son:

:mail: (PHPMailer) Puntero al objeto mail encargado del envío.
:emails: (string) Dirección de correo o lista de direcciones.
:emailsCC: (string) Dirección de correo o lista de direcciones con copia de cortesía.
:emailsBCC: (string) Dirección de correo o lista de direcciones con copia oculta.


getTemplateHtml
---------------

Genera y devuelve el mensaje a enviar en formato html. Para crear el mensaje utiliza una
plantilla Twig.

:params: (array) Lista de claves y valores que se aplican a la plantilla. Cada clave se
    corresponde al nombre de una variable definida en la plantilla. El valor es el valor con
    el que se reemplazará la variable.
:template: (string) Nombre de la plantilla Twig a utilizar.
:objects: (array) Lista de claves y valores que se pasan a la plantilla. Cada clave se
    corresponde al nombre de una variable que se podrá usar en plantilla. El valor es el
    la dirección al objeto que se corresponderá al usar la variable.


newMail
-------

Crea y nos retorna un objeto PHPMailer configurado con los datos de conexión
informados en las preferencia de la aplicación con el que podemos enviar un correo electrónico.


send
----

Envía el correo electrónico indicado en la llamada y nos retorna si se ha completado
correctamente o no el envío.


test
----

Nos permite realizar una conexión con nuestro servidor de correo para comprobar si los
datos de configuración del mail son correctos.
