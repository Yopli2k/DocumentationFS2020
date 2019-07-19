.. highlight:: rst
.. title:: Facturascripts Modelos para informes
.. meta::
  :http-equiv=Content-Type: text/html; charset=UTF-8
  :generator: FacturaScripts Documentacion
  :description: Modelo para informes
  :keywords: facturascripts, desarrollo, modelo, informe, report
  :robots: Index, Follow
  :author: Jose Antonio Cuello (Artex Trading)
  :subject: Modelos FacturaScripts
  :lang: es


#####################
Modelos para informes
#####################

.. important::
  Debido a que este modelo es **sólo para la visualización** de datos y para usar con el
  controlador **ReportController** tiene una estructura básica, no usando la estructura completa
  de los modelos de datos estándar.

Cuando deseamos realizar un informe donde vamos a procesar distintos modelos y presentar al
usuario el resultado del proceso usaremos este tipo de modelo. Su implementación básica
es muy sencilla y rápida, dejando al desarrollador la tarea de desarrollar el proceso principal
que es específica para cada informe.

Para diferenciar de los otros modelos de datos este tipo de modelo se deben guardar en la carpeta **Report**
dentro de la carpeta *Model* donde se encuentran todos los modelos. Esto es importante porque las vistas report
buscarán en esta carpeta (*Report*) los modelos.

También como recomendación, dado que el modelo puede contener muchas líneas de código (dependiendo de la
complejidad del cálculo de los resultados finales), separar en otra clase la estructura de datos. Normalmente
guardaremos esta clase dentro de una carpeta **Data** dentro de *Reports*.

Así para poder usar el modelo debemos:
    - crear una nueva clase en la carpeta *Model/Report/Data*
    - definir el *namespace* correspondiente respecto a nuestro plugin
    - declarar la lista de atributos o datos declarados como públicos

    - crear una nueva clase que hereda de *ModelReport* en la carpeta *Model/Report*
    - definir el *namespace* correspondiente respecto a nuestro plugin
    - usar la clase que define la estructura de datos
    - declarar el método obligatorio **all** que calcula y retorna un array de la clase de datos


.. Note::
    **Buenas prácticas para los nombres**
        El nombre de la clase del modelo debe ser siempre en singular y UpperCamelCase.

    **Nombres de columna conflictivos**
        FS2018 utiliza algunos nombres reservados. Evite usar en sus columnas nombres como: *active*, *action* y *code*.


Método obligatorio: all
=======================

Para un correcto funcionamiento del modelo, tenemos que retornar la estructura de datos a
visualizar en el informe. Para ello es obligatorio definir el método **all** que calcula el informe,
crea un array con cada uno de los registros a visualizar y lo retorna como resultado del método.

También es posible realizar obtener los datos introducidos por el usuario para el cálculo o para
comprobaciones iniciales. Este método recibe como parámetro la lista de filtros definidos en la vista, pudiendo
acceder al valor mediante el método **getValue** del filtro.

.. code::

    public function all($filters, $where, $order, $offset, $limit)
    {
        $idemployee = $filters['employee']->getValue();
        if (empty($idemployee)) {
            self::$miniLog->warning(self::$i18n->trans('no-employee-report'));
            return [];
        }

        $startdate = $filters['date']->getValue(PeriodFilter::STARTDATE_ID);
        if (empty($startdate)) {
            self::$miniLog->warning(self::$i18n->trans('no-period-report'));
            return [];
        }

        $enddate = $filters['date']->getValue(PeriodFilter::ENDDATE_ID);
        if (empty($enddate)) {
            $enddate = $startdate;
        }

        return $this->attendancesForEmployee($idemployee, $startdate, $enddate);
    }
