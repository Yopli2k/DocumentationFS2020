.. highlight:: rst
.. title:: Facturascripts primeros pasos: Tu primer cliente
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Primeros pasos. Como crear clientes en FacturaScripts 2018.
  :keywords: facturascripts, configurar, dar de alta, clientes
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Primer Cliente FacturaScripts 2018
  :lang: es

#################
Tu primer cliente
#################

La lista de cliente con los que trabajamos o hemos trabajado la encontrarmos en la opción del
menú (:guilabel:`Ventas->Clientes`). Esta lista, si no se han instalado datos de prueba, nos
aparecerá vacía. Para crear un nuevo cliente debemos hacer clic en el botón de
insertar (botón con fondo verde y signo *+*) y rellenamos los campos del formulario.

**Datos Generales**

:Código: Identificador interno del cliente
:Nombre: Nombre del cliente. Normalmente el nombre comercial con el que se conoce al cliente
:Razón Social: Nombre fiscal para facturas y otros documento oficiales
:Id. Fiscal: Tipo de identificador fiscal que tenemos del cliente
:Cif/Nif: Identificador fiscal del cliente
:Persona Física: *(Es una persona física)* Indica si el cliente es una empresa o una persona física a efectos fiscales

**Datos de Contacto**

:Dir. Factura: *(Direción de Facturación)* Identificador del contacto usado por defecto para la elaboración de facturas. Se debe elegir de la lista de contactos del cliente
:Dir. Envío: *(Direción de Envío)* Identificador del contacto usado por defecto para el envío de mercancía. Se debe elegir de la lista de contactos del cliente
:Teléfono: Número de teléfono general para contactar con el cliente
:Email: Correo electrónico para notificaciones

**Datos comerciales**

:Grupo: Identificador del grupo de cliente. Se debe elegir de la lista de grupos. (ver más adelante)
:Serie: Identificador de la serie de facturación por defecto a aplicar al crear un documento para el cliente
:Forma Pago: Método de pago y configuración de la fecha de pago
:Días Pago: Relación de días, separados por coma, en los que el cliente realiza el pago
:Agente: Agente comercial que gestiona este cliente
:IRPF: Porcentaje de retenciones físicas a aplicar en las facturas de venta
:Régimen IVA: Régimen de impuesto que se le aplica al cliente

Además de los campos anteriores, de manera opcional, podemos indicar la cuenta contable para
las ventas y cobros. Si no se informa se usará la cuenta establecida en niveles superiores
según el órden Cliente, Grupo, Empresa.

**Otros Datos**

:Fec. Creación: Fecha en la que se da de alta el cliente. (Se rellena automáticamente)
:Fec. Baja: Fecha en la que se cesa la relación comercial.
:De Baja: Indica si se puede utilizar el cliente para nuevos documentos.
:Observaciones: Indicaciones adicionales que se deseen guardar por escrito sobre el cliente.


Direcciones y Contactos
=======================

Este apartado engloba la lista de direcciones y personas de contacto con las que tratamos
del cliente. Las direcciones comerciales se dividen en las usadas para temas fiscales (normalmente una)
y las direcciones de envío de mercancía, normalmente porque el cliente tiene varios almacenes, tiendas, etc.

Podemos ver un listado de todas las direcciones y contactos al consultar los clientes, en la pestaña
adicional denominada **Direcciones y contactos**. En este listado podemos filtrar, consultar y modificar
los datos introducidos de una manera directa.

Para introducir nuevas direcciones o contactos también podemos hacerlo estando consultando la ficha de un
cliente podemos ver, en la parte izquierda, la opción (:guilabel:`Direcciones y contactos`) mostrándonos,
al pulsarla con el botón izquierdo del ratón la lista del cliente. Para crear una nueva dirección o persona
de contacto debemos hacer clic en el botón de insertar (botón con fondo verde y signo *+*) y rellenamos los
campos del formulario.

.. note::
    Los datos de este formulario son usados por el plugin CRM, no incluido en el software base.
    Por este motivo no son necesarios en todos los casos siendo muchos de ellos opcionales.


**Datos Generales**

:Descripción: Texto interno que nos permite identificar la dirección/contacto del cliente.
:Nombre: Nombre del contacto
:Apellidos: Apellidos del contacto
:Email: Correo electrónico para notificaciones
:Cif/Nif: Identificador fiscal del contacto
:Empresa: Nombre de la empresa del contacto
:Cargo: Cargo laboral que ocupa el contacto
:Teléfonos: Números de teléfono del contacto
:Cliente: Identificador que relaciona el contacto con el cliente al cual pertenece
:Proveedor: Identificador que relaciona el contacto con el proveedor al cual pertenece


**Otros Datos**

:Dirección: Dirección de localización del contacto
:Apartado: Información adicional
:Cód. Postal: Distrito postal de la dirección del contacto
:Ciudad: Identificador de la ciudad
:Provincia: Identificador de la provincia
:País: Identificador del país. Se debe elegir de la lista de países.
:Fec. Creación: Fecha en la que se da de alta el contacto. (Se rellena automáticamente)
:Ult. Conexión: Última fecha en la que se ha conectado al ERP. (Se rellena automáticamente)
:Puntos: Cantidad de puntos obtenidos en el proceso de fidelización
:Nivel: Nivel de acceso cuando se conecta al ERP
:Verificado: Indica si el contacto ha realizado correctamente el proceso de alta desde la web
:Persona Física: *(Es una persona física)* Indica si el contacto es una empresa o una persona física a efectos fiscales
:Marketing: *(Permite marketing)* Indica si el contacto permite envíos publicitarios
:Observaciones: Indicaciones adicionales que se deseen guardar por escrito sobre el contacto

Al pulsar el botón de guardar, habremos creado una nueva dirección o persona de contacto para el cliente.


Cuentas bancarias
=================

Estando consultando la ficha de un cliente podemos ver en la parte izquierda de la ventana la opción
(:guilabel:`Cuentas bancarias`) mostrándonos, al pulsarla con el botón izquierdo del ratón
la lista del cliente. Si deseamos añadir un nuevo registro, pulsaremos el botón *Nuevo*
desplegándose el formulario donde informar los valores:

:Descripción: Texto interno que nos permite identificar a la cuenta bancaria del cliente.
:Principal: Indica si es la cuenta bancaria por defecto a utilizar para el cliente.
:IBAN: Identificador bancario del cliente.
:SWIFT: Identificador bancario de la entidad bancaria usada por el cliente.
:Fecha Mandato: Fecha de la firma del mandato bancario obligatorio para poder realizar domiciliaciones.

Al pulsar el botón de guardar, habremos creado una nueva cuenta bancaria para el cliente.


Grupo de Clientes
=================

Podemos indicar que distintos clientes pertenecen a un mismo grupo de clientes. Esto es práctico
para informes posteriores y para la aplicación de condiciones comerciales a todos los clientes
de un mismo grupo.

El listado de todos los grupo creados se pueden consultar desde la opción del menú que muestra los clientes,
en la pestaña adicional denominada **Grupos**. En este listado podemos filtrar, consultar y modificar
los datos introducidos o crear nuevos grupos haciendo clic en el botón de insertar (botón con fondo verde
y signo *+*) y rellenamos los campos del formulario:

:Código: Identificador interno del grupo
:Descripción: Descripción que ayuda al usuario a identificar el grupo
:Grupo Padre: Permite establecer un órden de relación Padre->Hijo, pudiendo crear una jerarquía entre grupos

Además de los campos anteriores, de manera opcional, podemos indicar la cuenta contable para
las ventas y cobros. Si no se informa se usará la cuenta establecida en niveles superiores
según el órden Cliente, Grupo, Empresa.

Al pulsar el botón de guardar, habremos creado un nuevo grupo. Ahora podemos asignarlo a los clientes.
