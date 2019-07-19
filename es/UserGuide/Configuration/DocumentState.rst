.. highlight:: rst
.. title:: Facturascripts configurar: Estados de Documentos
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Configurar estados de documentos en FacturaScripts 2018.
  :keywords: facturascripts, configurar, estado, documento, estados de documentos
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Configurar Estados de Documentos FacturaScripts 2018
  :lang: es

#####################
Estados de Documentos
#####################

Los documentos de compra y de venta en muchas ocasiones necesitan disponer de estados: Emitido, Aceptado, Rechazado, etc,
modificar el stock, indicar si ese documento podrá ser editado o por el contrario ya no puede sufrir nuevos cambios.

Todos estos procesos en *FacturaScripts* se pueden configurar desde los estados de documentos, donde podemos
crear todos los estados por los que puede pasar cada uno de los documentos y personalizar las acciones
que la aplicación debe tomar.

Para consultar o modificar la lista de estados de documentos disponibles debemos ir a la opción del
menú (:guilabel:`Administrador->Estados de documentos`). Para crear un nuevo estado debemos hacer clic
en el botón de insertar (botón con fondo verde y signo *+*) y rellenamos los campos del formulario.

:Nombre: Indica el texto descriptivo del estado
:Documento: *(Tipo de documento)* Debemos seleccionar de la lista de documentos a cual tipo se aplica el estado
:Stock: *(Actualizar stock)* Indicamos que proceso se debe hacer con el stock al adquirir o dejar el estado el documento.

    +-------------------+---------------------------------------------------+
    | *Acción*          | *Descripción*                                     |
    +-------------------+---------------------------------------------------+
    | **No hacer nada** | No realiza ninguna actualización sobre el stock   |
    +-------------------+---------------------------------------------------+
    | **Reservar**      | Actualiza las cantidades reservadas               |
    +-------------------+---------------------------------------------------+
    | **Restar**        | Realiza el rebaje de stock                        |
    +-------------------+---------------------------------------------------+
    | **Añadir**        | Realiza la entrada de stock                       |
    +-------------------+---------------------------------------------------+
    | **Preveer**       | Actualiza las cantidades pendientes de recibir    |
    +-------------------+---------------------------------------------------+

:Generar: *(Generar tipo de documento)* Indica que tipo de documento se debe generar a partir del documento padre
:Editable: Indica si el documento será editable después de adquirir el estado
:Por Defecto: Marca el estado como por defecto. Normalmente para altas de documentos

Al pulsar el botón de guardar, habremos creado el estado de documento y estará disponible para su uso.
