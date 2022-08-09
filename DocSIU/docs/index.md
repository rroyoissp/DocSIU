# Documentación SIU IUSE-ISSP
---

##<u> Commits</u>
<br></br>
#### Sergio

##### **r30488 | sergio | 2019-04-09 17:00:57 -0300 (Tue, 09 Apr 2019)**
<br></br>
A /nodos/iuse/gestion/trunk/3.16.2
<br></br>


        
        class cuadro_seleccion_diferida extends guarani_pers_ei_cuadro
        {
                function inicializar($parametros=array())
                {parent::inicializar($parametros);
                // Si existe el evento 'seleccion' y es de disparo diferido, se alinea a izquierda de las columnas y se genera la utilidad "Todos/Ninguno".
                if ($this->existe_evento('seleccion')) {
                        $this->evento('seleccion')->set_disparo_diferido(true);
                        $this->evento('seleccion')->set_alineacion_pre_columnas(true);
                        $this->set_manejador_salida('html', 'cuadro_seleccion_diferida_salida_html');
                }
        }
        //-----------------------------------------------------------------------------------
        //---- JAVASCRIPT -------------------------------------------------------------------
        //-----------------------------------------------------------------------------------
 
        /**
         * Se redefine el metodo set_evento para que no marque con un estilo diferente las filas chequeadas.
         */
        function extender_objeto_js()
        {
                echo "
                //---- Eventos ---------------------------------------------
 
                {$this->objeto_js}.set_evento = function(evento, hacer_submit, input)
                {
                        if (typeof hacer_submit == 'undefined') {
                                hacer_submit = true;
                        }
                        ei.prototype.set_evento.call(this, evento, hacer_submit);
                }
                ";
        }

<br></br>
#### DCelestino

##### **r31220 | dcelestino | 2019-04-15 16:48:05 -0300 (Mon, 15 Apr 2019)** 
- _Se agregó reporte nuevo de Clases Diarias. Se modificó el reporte de Constancia de Alumno Regular. Se agregó pequeño script para posicionar el cursor en el cuadro de búsqueda al clickear sobre el menú._

<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini
        
    
    Archivo de configuración de la visualización del menú de la aplicación
    menu = #
    # es el número de menú, y los posibles valores de # son:
    0: Menú original de Toba.
    1: Menú estilo Windows.    
    2: Menú estilo KDE.
    
    
    menu = 1
<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml
    
    
    <?xml version="1.0" encoding="UTF-8"?>
    <jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd" name="guarani" pageWidth="595" pageHeight="842" whenNoDataType="NoDataSection" columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20" uuid="3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8">
        <property name="ireport.zoom" value="1.2100000000000002"/>
        <property name="ireport.x" value="6"/>
        <property name="ireport.y" value="48"/>
        <property name="ireport.zoom" value="1.0"/>
        <property name="ireport.x" value="0"/>
        <property name="ireport.y" value="0"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
        <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
        <parameter name="solicitud" class="java.lang.Integer">
                <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
        <queryString>
                <![CDATA[SELECT
        COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ' ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
        sga_propuestas.nombre AS propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
        sga_insc_cursada,
        sga_comisiones,
        sga_comisiones_bh,
        sga_asignaciones
        sga_asignaciones,
        sga_periodos_lectivos
        sga_clases_asistencia_acum
         WHERE
                sga_constancias_solicitud.solicitud = $P{solicitud}
                AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
                AND sga_insc_cursada.comision = sga_comisiones.comision
                AND sga_comisiones_bh.comision = sga_comisiones.comision
                AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
                AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
                AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
                AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
                /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
                AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
                AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
                 GROUP BY
                        sga_alumnos.legajo,
                        vw_personas.apellido,
                        <band splitType="Stretch"/>
                </columnHeader>
                <detail>
                       <band height="434" splitType="Stretch">
                       <band height="653" splitType="Stretch">
                                <textField isBlankWhenNull="true">
                                      <reportElement x="53" y="13" width="447" height="115" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                      <textElement textAlignment="Justified"/>
                                      <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                                </textField>
                        <line>
                                <reportElement x="185" y="250" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                        <textField isBlankWhenNull="true">
                                <reportElement x="53" y="139" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="147" y="271" width="261" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="147" y="251" width="261" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                        </textField>
                        <textField>
                                <reportElement x="134" y="328" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                        </textField>
                        <image>
                                <reportElement x="213" y="199" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                        </image>
                        <textField>
                                <reportElement x="83" y="363" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                        </textField>
                        <staticText>
                                <reportElement x="147" y="291" width="261" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                <textElement textAlignment="Center"/>
                                <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                <text><![CDATA[IUSE]]></text>
                        </staticText>
                        <image>
                                <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                                <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                        </image>
                </band>
        </detail>
        <columnFooter>

<br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/personalizacion.ini
    
    -iniciada = "no"
    +iniciada = "si"
      schema_personalizado = "toba_guarani_pers"
      schema_original = "desarrollo"

A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co_clases_diarias.php
     
     class co_clases_diarias
     {

       function get_listado_vista()
       function get_listado_vista($filtro='')
        {


                /*$hoy = toba::db()->quote(guarani_fecha::get_hoy());
                $formato_fecha_hora_visual = toba::db()->quote(comunes::formato_fecha_hora_visual);*/

               if ($filtro) {
                       $where .= " AND $filtro ";
               }


                $sql = "SELECT
               '' as firma,
        sga_clases.clase,
        sga_asignaciones.dia_semana AS dia_semana,
       sga_clases.fecha AS fecha_clase,
       to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
       sga_clases.fecha,
        to_char(
                sga_asignaciones.hora_inicio,
                       'HH24:MI'
                       sga_asignaciones.hora_finalizacion,
                       'HH24:MI'
               ) AS hora_finalizacion,
              /*sga_clases.tema_planificado,
              /*sga_clases.tema_planificado,*/sga_clases.tema_dictado,sga_clases.cantidad_horas_dictadas,
              /*sga_clases.cantidad_horas_dictadas,sga_clases_tipos.nombre AS tipo_clase_nombre
              */sga_espacios.nombre AS espacio_nombre,sga_comisiones.nombre AS nombre_comision,
               vw_actividades.nombre AS nombre_actividad,
              /*     sga_comisiones.comision,*/
               sga_propuestas.nombre AS propuesta,
       CONCAT(mdp_personas.apellido,' ', mdp_personas.nombres) as \"docente_nombre\"
              sga_propuestas.propuesta AS idpropuesta,
       array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \"docente_nombre\"

        FROM
               sga_comisiones,

        AND sga_clases.banda_horaria = sga_comisiones_bh.banda_horaria
        AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
        AND sga_clases.valido = 1
       AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE
       /* igual a fecha de hoy AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE*/
        AND sga_comisiones.comision = sga_comisiones_bh.comision
        AND vw_actividades.elemento = sga_comisiones.elemento
        AND sga_comisiones_propuestas.comision = sga_comisiones.comision
        AND sga_docentes_comision.comision = sga_comisiones.comision
        AND sga_docentes.docente = sga_docentes_comision.docente
        AND sga_docentes.persona = mdp_personas.persona
       AND mdp_personas.usuario <> 'Administracion'
       $where

       GROUP BY
              sga_clases.fecha,
              sga_asignaciones.hora_inicio,
              sga_asignaciones.dia_semana,
              sga_clases.fecha,
              sga_asignaciones.hora_inicio,
              sga_asignaciones.hora_finalizacion,
              sga_espacios.nombre,
              sga_comisiones.nombre ,
              vw_actividades.nombre,
              sga_propuestas.nombre,
              sga_clases.clase,
              sga_propuestas.propuesta
        ORDER BY
               sga_clases.fecha,
               sga_asignaciones.hora_inicio
                                  ";
                          //die($sql);
                       return guarani_db::consultar($sql);
               }

       A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas
       A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas/ci_rep_clases_diarias.php
       class ci_rep_clases_diarias extends ci_reporte
        {
               protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
              /*protected $s__filtro_estado;
              protected $s__filtro_estado_rechazadas;*/
              protected $s__filtro_estado;
              protected $s__filtro_estado_rechazadas;

               //--------------------------------------------------------------------------
               //---- filtro --------------------------------------------------------------


               function conf__filtro(toba_ei_filtro $filtro)
               {

                      if (isset($this->s__datos)) {
                       $filtro->set_datos($this->s__datos);
                      }


               }

               /**
                       */
               function evt__filtro__filtrar($datos)
               {

                      if (isset($datos)) {
                              $this->s__datos = $datos;
                              $filtro = $filtro_modalidad . $filtro_ras;
                              $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
                      } else {
                              unset($this->s__datos);
                              $this->s__filtro = '';
                      }
               }
       
               function conf__cuadro(toba_ei_cuadro $cuadro)
               {
                      $datos = $this->get_datos();
                      $cuadro->set_datos($datos);
                      $cuadro->set_eof_mensaje($this->get_msg_eof());

                      /*
                      Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
                      if (isset($this->s__datos)) {
                              $datos = $this->get_datos($this->s__filtro);
                              $cuadro->set_datos($datos);
                              $cuadro->set_eof_mensaje($this->get_msg_eof());
                      } elseif (toba::zona()->cargada()) {
                              $datos = $this->get_datos('sga_comisiones.comision = ' . toba::zona()->get_editable());
                              $cuadro->set_datos($datos);
                              $cuadro->set_eof_mensaje($this->get_msg_eof());
                      } else {
                              $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
                      }
                       $cuadro->set_filtro_asociado($this->dep('filtro'));
                      */
               }
       
               function get_tabla_principal()
               {
                      //return 'sga_insc_cursada';
                      return 'sga_clases';
               }

              function get_datos($filtros = null)
              function get_datos($filtro)
               {
                      return toba::consulta_php('co_clases_diarias')->get_listado_vista();
                      return toba::consulta_php('co_clases_diarias')->get_listado_vista($filtro);
               }

       }


              }        
##### **r31221 | dcelestino | 2019-04-15 17:43:41 -0300 (Mon, 15 Apr 2019)**
- _Merge de personalizaciones en testing._
<br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani_clases_consultas_nuevas.php
<br></br>
    
    
         static $clases = array(
               'co_clases_diarias' => array('clase'=>'co_clases_diarias','path'=>'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
               'co_ctrl_inasistencias' => array('clase'=>'co_ctrl_inasistencia','path'=>'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
               'co_inasistencias' => array('clase'=>'co_inasistencias','path'=>'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
               'co_inscripciones' => array('clase'=>'co_inscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
               'co_inscripciones_cursadas' => array('clase'=>'co_inscripciones_cursadas','path'=>'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
               'co_inscriptos' => array('clase'=>'co_inscriptos','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
               'co_mesas_de_examen' => array('clase'=>'co_mesas_de_examen','path'=>'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
               'co_preinscripciones' => array('clase'=>'co_preinscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
               'co_requisitos_ingreso' => array('clase'=>'co_requisitos_ingreso','path'=>'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
               'co_usuarios' => array('clase'=>'co_usuarios_pers','path'=>'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
        );

<br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co_clases_diarias.php
<br></br>
    
    
    class co_clases_diarias
    {

       function get_listado_vista($filtro='')
       {
               /*$hoy = toba::db()->quote(guarani_fecha::get_hoy());
               $formato_fecha_hora_visual = toba::db()->quote(comunes::formato_fecha_hora_visual);*/

               if ($filtro) {
                       $where .= " AND $filtro ";
               }


               $sql = "SELECT
               '' as firma,
       sga_clases.clase,
       sga_asignaciones.dia_semana AS dia_semana,
       to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
       sga_clases.fecha,
       to_char(
               sga_asignaciones.hora_inicio, 'HH24:MI'
               ) AS hora_inicio,
       to_char(
               sga_asignaciones.hora_finalizacion, 'HH24:MI'
               ) AS hora_finalizacion,
       /*sga_clases.tema_planificado,*/
     sga_clases.tema_dictado,
     /*sga_clases.cantidad_horas_dictadas,
     sga_clases_tipos.nombre AS tipo_clase_nombre,*/
       sga_espacios.nombre AS espacio_nombre,
       sga_comisiones.nombre AS nombre_comision,
       vw_actividades.nombre AS nombre_actividad,
       /*sga_comisiones.comision,
       */sga_propuestas.nombre AS propuesta,
       sga_propuestas.propuesta AS idpropuesta,
        array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \"docente_nombre\"

    FROM
       sga_comisiones,
       mdp_personas,
       sga_docentes_comision,
       sga_docentes,
       sga_comisiones_propuestas,
       vw_actividades,
       sga_propuestas,
       sga_comisiones_bh,
       sga_clases,
       sga_clases_tipos,
       sga_asignaciones
    LEFT JOIN sga_espacios ON sga_asignaciones.espacio = sga_espacios.espacio
    WHERE
       /*sga_comisiones_bh.comision = '1'
    AND */
       sga_comisiones_bh.tipo_clase = sga_clases_tipos.tipo_clase
    AND sga_clases.banda_horaria = sga_comisiones_bh.banda_horaria
    AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
    AND sga_clases.valido = 1
    /* igual a fecha de hoy AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE*/
    +AND sga_comisiones.comision = sga_comisiones_bh.comision
    AND vw_actividades.elemento = sga_comisiones.elemento
    AND sga_comisiones_propuestas.comision = sga_comisiones.comision
    AND sga_comisiones_propuestas.propuesta = sga_propuestas.propuesta
    AND sga_docentes_comision.comision = sga_comisiones.comision
    AND sga_docentes.docente = sga_docentes_comision.docente
    +AND sga_docentes.persona = mdp_personas.persona
    AND mdp_personas.usuario <> 'Administracion'
    $where

       GROUP BY
       sga_clases.fecha,
       sga_asignaciones.hora_inicio,
       sga_asignaciones.dia_semana,
       sga_clases.fecha,
       sga_asignaciones.hora_inicio,
       sga_asignaciones.hora_finalizacion,
       sga_espacios.nombre,
       sga_comisiones.nombre ,
       vw_actividades.nombre,
       sga_propuestas.nombre,
       sga_clases.clase,
       sga_propuestas.propuesta
    ORDER BY
       sga_clases.fecha,
       sga_asignaciones.hora_inicio
                          ";
                          //die($sql);
               return guarani_db::consultar($sql);
       }

    }
<br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas
<br></br>
    
    
    class ci_rep_clases_diarias extends ci_reporte
    {
       protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
       protected $s__filtro_estado;
       protected $s__filtro_estado_rechazadas;

       //--------------------------------------------------------------------------
       //---- filtro --------------------------------------------------------------
       //--------------------------------------------------------------------------

       function conf__filtro(toba_ei_filtro $filtro)
       {
               if (isset($this->s__datos)) {
                       $filtro->set_datos($this->s__datos);
               }


       }

       /**
               * Redefinición del evento filtrar, para que arme una cadena WHERE acorde con la
               * nueva estructura de modalidades de cursada de comisión.
              */
       function evt__filtro__filtrar($datos)
       {
               if (isset($datos)) {
                       $this->s__datos = $datos;
                       $filtro = $filtro_modalidad . $filtro_ras;
                      $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
               } else {
                       unset($this->s__datos);
                       $this->s__filtro = '';
               }
       }

       function conf__cuadro(toba_ei_cuadro $cuadro)
       {
               if (isset($this->s__datos)) {
                       $datos = $this->get_datos($this->s__filtro);
                      $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } elseif (toba::zona()->cargada()) {
                       $datos = $this->get_datos('sga_comisiones.comision = ' . toba::zona()->get_editable());
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } else {
                       $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
               }
               $cuadro->set_filtro_asociado($this->dep('filtro'));
       }
       function get_tabla_principal()
       {
               return 'sga_clases';
       }

       function get_datos($filtro)
       {
               return toba::consulta_php('co_clases_diarias')->get_listado_vista($filtro);
       }

       }
<br></br>
##### **r31228 | dcelestino | 2019-04-16 12:02:19 -0300 (Tue, 16 Apr 2019)**
- _Se agregó reporte nuevo de Clases Diarias. Se modificó el reporte de Constancia de Alumno Regular. Se agregó pequeño script para posicionar el cursor en el cuadro de búsqueda al clickear sobre el menú._

<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini
          
        
    Archivo de configuración de la visualización del menú de la aplicación
    menu = #
    # es el número de menú, y los posibles valores de # son:
    0: Menú original de Toba.
    1: Menú estilo Windows.    
    2: Menú estilo KDE.
    
    
    menu = 1
<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml
    
    
    <?xml version="1.0" encoding="UTF-8"?>
    <jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd" name="guarani" pageWidth="595" pageHeight="842" whenNoDataType="NoDataSection" columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20" uuid="3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8">
        <property name="ireport.zoom" value="1.2100000000000002"/>
        <property name="ireport.x" value="6"/>
        <property name="ireport.y" value="48"/>
        <property name="ireport.zoom" value="1.0"/>
        <property name="ireport.x" value="0"/>
        <property name="ireport.y" value="0"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
        <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
        <parameter name="solicitud" class="java.lang.Integer">
                <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
        <queryString>
                <![CDATA[SELECT
        COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ' ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
        sga_propuestas.nombre AS propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
        sga_insc_cursada,
        sga_comisiones,
        sga_comisiones_bh,
        sga_asignaciones
        sga_asignaciones,
        sga_periodos_lectivos
        sga_clases_asistencia_acum
         WHERE
                sga_constancias_solicitud.solicitud = $P{solicitud}
                AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
                AND sga_insc_cursada.comision = sga_comisiones.comision
                AND sga_comisiones_bh.comision = sga_comisiones.comision
                AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
                AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
                AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
                AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
                /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
                AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
                AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
                 GROUP BY
                        sga_alumnos.legajo,
                        vw_personas.apellido,
                        <band splitType="Stretch"/>
                </columnHeader>
                <detail>
                       <band height="434" splitType="Stretch">
                       <band height="653" splitType="Stretch">
                                <textField isBlankWhenNull="true">
                                      <reportElement x="53" y="13" width="447" height="115" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                      <textElement textAlignment="Justified"/>
                                      <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                                </textField>
                        <line>
                                <reportElement x="185" y="250" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                        <textField isBlankWhenNull="true">
                                <reportElement x="53" y="139" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="147" y="271" width="261" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="147" y="251" width="261" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                        </textField>
                        <textField>
                                <reportElement x="134" y="328" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                        </textField>
                        <image>
                                <reportElement x="213" y="199" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                        </image>
                        <textField>
                                <reportElement x="83" y="363" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                        </textField>
                        <staticText>
                                <reportElement x="147" y="291" width="261" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                <textElement textAlignment="Center"/>
                                <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                <text><![CDATA[IUSE]]></text>
                        </staticText>
                        <image>
                                <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                                <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                        </image>
                </band>
        </detail>
        <columnFooter>

              }
<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas

    class ci_rep_clases_diarias extends ci_reporte
    {
        protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
       /*protected $s__filtro_estado;
       protected $s__filtro_estado_rechazadas;*/
       protected $s__filtro_estado;
       protected $s__filtro_estado_rechazadas;

        //--------------------------------------------------------------------------
        //---- filtro --------------------------------------------------------------


        function conf__filtro(toba_ei_filtro $filtro)
        {

               if (isset($this->s__datos)) {
                       $filtro->set_datos($this->s__datos);
               }

        }

        /**

                */
        function evt__filtro__filtrar($datos)
        {

               if (isset($datos)) {
                       $this->s__datos = $datos;
                       $filtro = $filtro_modalidad . $filtro_ras;
                       $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
               } else {
                       unset($this->s__datos);
                       $this->s__filtro = '';
               }
        }

        function conf__cuadro(toba_ei_cuadro $cuadro)
        {
               $datos = $this->get_datos();
               $cuadro->set_datos($datos);
               $cuadro->set_eof_mensaje($this->get_msg_eof());

               /*
               Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
               if (isset($this->s__datos)) {
                       $datos = $this->get_datos($this->s__filtro);
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } elseif (toba::zona()->cargada()) {
                       $datos = $this->get_datos('sga_comisiones.comision = ' . toba::zona()->get_editable());
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } else {
                       $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
               }
                $cuadro->set_filtro_asociado($this->dep('filtro'));
               */
        }

        function get_tabla_principal()
        {
               //return 'sga_insc_cursada';
               return 'sga_clases';
        }

       function get_datos($filtros = null)
       function get_datos($filtro)
        {
               return toba::consulta_php('co_clases_diarias')->get_listado_vista();
               return toba::consulta_php('co_clases_diarias')->get_listado_vista($filtro);
        }

    }


       }

A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas/ci_rep_clases_diarias.php

       
    class ci_rep_clases_diarias extends ci_reporte
        {
               protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
              /*protected $s__filtro_estado;
              protected $s__filtro_estado_rechazadas;*/
              protected $s__filtro_estado;
              protected $s__filtro_estado_rechazadas;

               //--------------------------------------------------------------------------
               //---- filtro --------------------------------------------------------------


               function conf__filtro(toba_ei_filtro $filtro)
               {

                      if (isset($this->s__datos)) {
                       $filtro->set_datos($this->s__datos);
                      }


               }

               /**
                       */
               function evt__filtro__filtrar($datos)
               {

                      if (isset($datos)) {
                              $this->s__datos = $datos;
                              $filtro = $filtro_modalidad . $filtro_ras;
                              $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
                      } else {
                              unset($this->s__datos);
                              $this->s__filtro = '';
                      }
               }
       
               function conf__cuadro(toba_ei_cuadro $cuadro)
               {
                      $datos = $this->get_datos();
                      $cuadro->set_datos($datos);
                      $cuadro->set_eof_mensaje($this->get_msg_eof());

                      /*
                      Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
                      if (isset($this->s__datos)) {
                              $datos = $this->get_datos($this->s__filtro);
                              $cuadro->set_datos($datos);
                              $cuadro->set_eof_mensaje($this->get_msg_eof());
                      } elseif (toba::zona()->cargada()) {
                              $datos = $this->get_datos('sga_comisiones.comision = ' . toba::zona()->get_editable());
                              $cuadro->set_datos($datos);
                              $cuadro->set_eof_mensaje($this->get_msg_eof());
                      } else {
                              $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
                      }
                       $cuadro->set_filtro_asociado($this->dep('filtro'));
                      */
               }
       
               function get_tabla_principal()
               {
                      //return 'sga_insc_cursada';
                      return 'sga_clases';
               }

              function get_datos($filtros = null)
              function get_datos($filtro)
               {
                      return toba::consulta_php('co_clases_diarias')->get_listado_vista();
                      return toba::consulta_php('co_clases_diarias')->get_listado_vista($filtro);
               }

       }


              }
<br></br>
##### **r31232 | dcelestino | 2019-04-16 15:02:10 -0300 (Tue, 16 Apr 2019)** 
- _Corrección reporte CAR._

D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co_clases_diarias.php
class co_clases_diarias
{

       function get_listado_vista($filtro='')
       {
               /*$hoy = toba::db()->quote(guarani_fecha::get_hoy());
               $formato_fecha_hora_visual = toba::db()->quote(comunes::formato_fecha_hora_visual);*/

               if ($filtro) {
                       $where .= " AND $filtro ";
               }


               $sql = "SELECT
               '' as firma,
       sga_clases.clase,
      sga_asignaciones.dia_semana AS dia_semana,
       to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
       sga_clases.fecha,
       to_char(
               sga_asignaciones.hora_inicio,
               'HH24:MI'
       ) AS hora_inicio,
       to_char(
               sga_asignaciones.hora_finalizacion,
               'HH24:MI'
       ) AS hora_finalizacion,
       /*sga_clases.tema_planificado,*/sga_clases.tema_dictado,/*sga_clases.cantidad_horas_dictadas,sga_clases_tipos.nombre AS tipo_clase_nombre,*/sga_espacios.nombre AS espacio_nombre,sga_comisiones.nombre AS nombre_comision,vw_actividades.nombre AS nombre_actividad,/*sga_comisiones.comision,*/sga_propuestas.nombre AS propuesta,sga_propuestas.propuesta AS idpropuesta,array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \"docente_nombre\"

        FROM
           sga_comisiones,
           mdp_personas,
           sga_docentes_comision,
           sga_docentes,
           sga_comisiones_propuestas,
           vw_actividades,
           sga_propuestas,
           sga_comisiones_bh,
           sga_clases,
           sga_clases_tipos,
           sga_asignaciones
    	   LEFT JOIN sga_espacios ON sga_asignaciones.espacio = sga_espacios.espacio
        WHERE
           /*sga_comisiones_bh.comision = '1'
        AND */
            sga_comisiones_bh.tipo_clase = sga_clases_tipos.tipo_clase
            AND sga_clases.banda_horaria = sga_comisiones_bh.banda_horaria
            AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
            AND sga_clases.valido = 1
            /* igual a fecha de hoy AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE*/
            AND sga_comisiones.comision = sga_comisiones_bh.comision
            AND vw_actividades.elemento = sga_comisiones.elemento
            AND sga_comisiones_propuestas.comision = sga_comisiones.comision
            AND sga_comisiones_propuestas.propuesta = sga_propuestas.propuesta
            AND sga_docentes_comision.comision = sga_comisiones.comision
            AND sga_docentes.docente = sga_docentes_comision.docente
            AND sga_docentes.persona = mdp_personas.persona
            AND mdp_personas.usuario <> 'Administracion'
        $where

        GROUP BY
           sga_clases.fecha,
           sga_asignaciones.hora_inicio,
           sga_asignaciones.dia_semana,
           sga_clases.fecha,
           sga_asignaciones.hora_inicio,
           sga_asignaciones.hora_finalizacion,
           sga_espacios.nombre,
           sga_comisiones.nombre ,
           vw_actividades.nombre,
           sga_propuestas.nombre,
           sga_clases.clase,
           sga_propuestas.propuesta
        ORDER BY
           sga_clases.fecha,
           sga_asignaciones.hora_inicio
                          ";
                          //die($sql);
               return guarani_db::consultar($sql);
       }

    }
<br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas
     
    class ci_rep_clases_diarias extends ci_reporte
    {
       protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
       protected $s__filtro_estado;
       protected $s__filtro_estado_rechazadas;

       //--------------------------------------------------------------------------
       //---- filtro --------------------------------------------------------------
       //--------------------------------------------------------------------------

       function conf__filtro(toba_ei_filtro $filtro)
       {
               if (isset($this->s__datos)) {
                       $filtro->set_datos($this->s__datos);
               }


       }

       /**
               * Redefinición del evento filtrar, para que arme una cadena WHERE acorde con la
               * nueva estructura de modalidades de cursada de comisión.
               */
       function evt__filtro__filtrar($datos)
       {
               if (isset($datos)) {
                       $this->s__datos = $datos;
                       $filtro = $filtro_modalidad . $filtro_ras;
                       $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
               } else {
                       unset($this->s__datos);
                       $this->s__filtro = '';
               }
       }

       function conf__cuadro(toba_ei_cuadro $cuadro)
       {
               if (isset($this->s__datos)) {
                       $datos = $this->get_datos($this->s__filtro);
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } elseif (toba::zona()->cargada()) {
                       $datos = $this->get_datos('sga_comisiones.comision = ' . toba::zona()->get_editable());
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } else {
                       $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
               }
               $cuadro->set_filtro_asociado($this->dep('filtro'));
       }

       function get_tabla_principal()
       {
               return 'sga_clases';
       }

       function get_datos($filtro)
       {
               return toba::consulta_php('co_clases_diarias')->get_listado_vista($filtro);
       }

       }
<br></br>
##### **r31233 | dcelestino | 2019-04-16 15:24:01 -0300 (Tue, 16 Apr 2019)**
- _Add personalizaciones._

<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini
    Archivo de configuración de la visualización del menú de la aplicación

    menú = #
    # es el número de menú, y los posibles valores de # son:

    0: Menú original de Toba.
    1: Menú estilo Windows.
    2: Menú estilo KDE.
<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co_clases_diarias.php
              
              
       class co_clases_diarias
       {
       function get_listado_vista()
       function get_listado_vista($filtro='')
       {
                /*$hoy = toba::db()->quote(guarani_fecha::get_hoy());
                $formato_fecha_hora_visual = toba::db()->quote(comunes::formato_fecha_hora_visual);*/

        if ($filtro) {
                   $where .= " AND $filtro ";
        }


                   $sql = "SELECT
                      '' as firma,
               sga_clases.clase,
               sga_asignaciones.dia_semana AS dia_semana,
              sga_clases.fecha AS fecha_clase,
              to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
              sga_clases.fecha,
               to_char(
                       sga_asignaciones.hora_inicio,
                       'HH24:MI'
                       sga_asignaciones.hora_finalizacion,
                       'HH24:MI'
               ) AS hora_finalizacion,
              /*sga_clases.tema_planificado,
              /*sga_clases.tema_planificado,*/
        sga_clases.tema_dictado,
       sga_clases.cantidad_horas_dictadas,
       /*sga_clases.cantidad_horas_dictadas,
         sga_clases_tipos.nombre AS tipo_clase_nombre,*/
               sga_espacios.nombre AS espacio_nombre,
               sga_comisiones.nombre AS nombre_comision,
               vw_actividades.nombre AS nombre_actividad,
        /*     sga_comisiones.comision,*/
               sga_propuestas.nombre AS propuesta,
       CONCAT(mdp_personas.apellido,' ', mdp_personas.nombres) as \"docente_nombre\"
              sga_propuestas.propuesta AS idpropuesta,
       array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \"docente_nombre\"

        FROM
        sga_comisiones,
              AND sga_clases.banda_horaria = sga_comisiones_bh.banda_horaria
              AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
              AND sga_clases.valido = 1
              AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE
              /* igual a fecha de hoy AND sga_clases.fecha = NOW() :: TIMESTAMP :: DATE*/
              AND sga_comisiones.comision = sga_comisiones_bh.comision
              AND vw_actividades.elemento = sga_comisiones.elemento
              AND sga_comisiones_propuestas.comision = sga_comisiones.comision
              AND sga_docentes_comision.comision = sga_comisiones.comision
              AND sga_docentes.docente = sga_docentes_comision.docente
              AND sga_docentes.persona = mdp_personas.persona
              AND mdp_personas.usuario <> 'Administracion'
       $where

       GROUP BY
              sga_clases.fecha,
              sga_asignaciones.hora_inicio,
              sga_asignaciones.dia_semana,
              sga_clases.fecha,
              sga_asignaciones.hora_inicio,
              sga_asignaciones.hora_finalizacion,
              sga_espacios.nombre,
              sga_comisiones.nombre ,
              vw_actividades.nombre,
              sga_propuestas.nombre,
              sga_clases.clase,
              sga_propuestas.propuesta
       ORDER BY
              sga_clases.fecha,
              sga_asignaciones.hora_inicio
                           ";
                          //die($sql);
                return guarani_db::consultar($sql);
        }
<br></br>
##### `r31549` 
- _Se versionan nuevamente las mismas personalizaciones: reporte de clases diarias y reporte CAR._

<br></br>
##### `r31565`
- _Se aplican personalizaciones anteriores._

<br></br>
##### `r31592` 
- _Mismas personalizaciones._

<br></br>
##### **r31800 | dcelestino | 2019-04-16 15:24:01 -0300 (Tue, 16 Apr 2019)**
- _Se agrego filtro por propuesta al reporte de mesas de examenes; también, el campo email al reporte de inscripciones a cursadas._

<br></br>
    
    static $clases = array(
                   'co_clases_diarias' => array('clase'=>'co_clases_diarias','path'=>'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
                   'co_ctrl_inasistencias' => array('clase'=>'co_ctrl_inasistencia','path'=>'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
                   'co_inasistencias' => array('clase'=>'co_inasistencias','path'=>'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
                   'co_inscripciones' => array('clase'=>'co_inscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
                   'co_inscripciones_cursadas' => array('clase'=>'co_inscripciones_cursadas','path'=>'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
                   'co_inscriptos' => array('clase'=>'co_inscriptos','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
                   'co_mesas_de_examen' => array('clase'=>'co_mesas_de_examen','path'=>'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
                   'co_preinscripciones' => array('clase'=>'co_preinscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
                   'co_requisitos_ingreso' => array('clase'=>'co_requisitos_ingreso','path'=>'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
                   'co_usuarios' => array('clase'=>'co_usuarios_pers','path'=>'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
            );
     }
<br></br>
##### `r31801` 
- _Se agrego filtro por propuesta al reporte de mesas de examenes; también, el campo email al reporte de inscripciones a cursadas._

<br></br>
##### **r31839 | dcelestino | 2019-05-10 13:28:53 -0300 (Fri, 10 May 2019)**
- _Reporte de mesas de examenes y reporte de inscripcion a cursadas._

<br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani_clases_consultas_nuevas.php
       
     static $clases = array(
                    'co_clases_diarias' => array('clase'=>'co_clases_diarias','path'=>'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
                   'co_ctrl_inasistencias' => array('clase'=>'co_ctrl_inasistencia','path'=>'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
                   'co_inasistencias' => array('clase'=>'co_inasistencias','path'=>'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
                   'co_inscripciones' => array('clase'=>'co_inscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
                'co_inscripciones_cursadas' => array('clase'=>'co_inscripciones_cursadas','path'=>'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
                   'co_inscriptos' => array('clase'=>'co_inscriptos','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
                   'co_mesas_de_examen' => array('clase'=>'co_mesas_de_examen','path'=>'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
                   'co_preinscripciones' => array('clase'=>'co_preinscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
                   'co_requisitos_ingreso' => array('clase'=>'co_requisitos_ingreso','path'=>'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
                   'co_usuarios' => array('clase'=>'co_usuarios_pers','path'=>'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
            );
     }

A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php
    
                $sql = "SELECT           -- Grupo 1
                                                            sga_ubicaciones.ubicacion,
                                                            sga_propuestas.propuesta,
                                                            sga_propuestas.nombre as propuesta_nombre,
                                                            sga_ubicaciones.nombre as ubicacion_nombre,
                                         -- Grupo 2
                                                            vw_actividades.elemento,

<br></br>
##### **r32677 | dcelestino | 2019-06-25 10:11:19 -0300 (Tue, 25 Jun 2019)**
- _Personalizaciones varias de reportes._

<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/logs/conflictos.log
     
    Postgres dijo: ERROR:  duplicate key value violates unique constraint "apex_consulta_php_pk"
    DETAIL:  Key (consulta_php, proyecto)=(2137000001, guarani) already exists..
    El sql conflictivo es: INSERT INTO apex_consulta_php (proyecto,consulta_php,clase,archivo_clase,archivo,punto_montaje) VALUES ('guarani','2137000001','co_clases_diarias','co_clases_diarias','nucleo/cursadas/co_clases_diarias.php','34000001')
       Errores recuperables
               [W:5] El update se hizo de <punto_montaje:1> a <punto_montaje:34000001>. Ahora el valor original de la columna es <punto_montaje:34000001>. El registro afectado tiene clave <consulta_php:41000006> en la tabla <apex_consulta_php>
               [W:5] El update se hizo de <punto_montaje:1> a <punto_montaje:34000001>. Ahora el valor original de la columna es <punto_montaje:34000001>. El registro afectado tiene clave <consulta_php:38000019> en la tabla <apex_consulta_php>
    Conflictos del archivo comp_2137000001.xml
        Errores fatales
                [F:2] Error de constraints en la tabla apex_objeto.
    Postgres dijo: ERROR:  duplicate key value violates unique constraint "apex_item_consumo_obj_pk"
    DETAIL:  Key (proyecto, item, objeto)=(guarani, 2137000008, 2137000006) already exists..
    El sql conflictivo es: INSERT INTO apex_item_objeto (proyecto,item,objeto,orden) VALUES ('guarani','2137000008','2137000006','1')
    Conflictos del archivo comp_41000059.xml
       Errores fatales
               [F:2] Error de constraints en la tabla apex_objeto_ei_cuadro_columna.
    El error no fue reconocido por el importador.
    Postgres dijo: ERROR:  duplicate key value violates unique constraint "apex_obj_ei_cuadro_pk"
    DETAIL:  Key (objeto_cuadro_col, objeto_cuadro, objeto_cuadro_proyecto)=(2137000013, 41000059, guarani) already exists..
    El sql conflictivo es: INSERT INTO apex_objeto_ei_cuadro_columna (objeto_cuadro_proyecto,objeto_cuadro,objeto_cuadro_col,clave,orden,titulo,estilo_titulo,estilo,ancho,formateo,no_ordenar,total,usar_vinculo,permitir_html) VALUES ('guarani','41000059','2137000013','emails','7','Email','ei-cuadro-col-tit','4','10%','1','0','0','0','0')
       Errores recuperables
               [W:5] El update se hizo de <ancho:25%> a <ancho:20%>. Ahora el valor original de la columna es <ancho:20%>. El registro afectado tiene clave <objeto_cuadro_proyecto:guarani,objeto_cuadro:41000059,objeto_cuadro_col:41000029> en la tabla <apex_objeto_ei_cuadro_columna>
               [W:5] El update se hizo de <ancho:25%> a <ancho:20%>. Ahora el valor original de la columna es <ancho:20%>. El registro afectado tiene clave <objeto_cuadro_proyecto:guarani,objeto_cuadro:41000059,objeto_cuadro_col:41000032> en la tabla <apex_objeto_ei_cuadro_columna>
    Conflictos del archivo comp_41000302.xml
       Errores fatales
               [F:2] Error de constraints en la tabla apex_objeto_ei_filtro_col.
    El error no fue reconocido por el importador.
    Postgres dijo: ERROR:  duplicate key value violates unique constraint "apex_ei_filtro_col_pk"
    DETAIL:  Key (objeto_ei_filtro_col, objeto_ei_filtro, objeto_ei_filtro_proyecto)=(2137000017, 41000302, guarani) already exists..
    El sql conflictivo es: INSERT INTO apex_objeto_ei_filtro_col (objeto_ei_filtro_col,objeto_ei_filtro,objeto_ei_filtro_proyecto,tipo,nombre,expresion,etiqueta,obligatorio,inicial,orden,opciones_es_multiple,opciones_ef,carga_metodo,carga_consulta_php,carga_fuente,carga_col_clave,carga_col_desc,carga_permite_no_seteado,carga_no_seteado_ocultar,punto_montaje) VALUES ('2137000017','41000302','guarani','opciones','propuesta','sga_propuestas.propuesta','Propuesta','0','1','9','0','ef_combo','get_listado','5','guarani','propuesta','nombre','0','0','1')
    Conflictos del archivo comp_41000119.xml
        Errores recuperables
                [W:5] El update se hizo de <menu:0> a <menu:1>. Ahora el valor original de la columna es <menu:1>. El registro afectado tiene clave <proyecto:guarani,item:41000119> en la tabla <apex_item>

M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani_clases_consultas_nuevas.php
     
    static $clases = array(
                'co_clases_diarias' => array('clase'=>'co_clases_diarias','path'=>'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
                'co_ctrl_inasistencias' => array('clase'=>'co_ctrl_inasistencia','path'=>'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
                'co_inasistencias' => array('clase'=>'co_inasistencias','path'=>'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
                'co_inscripciones' => array('clase'=>'co_inscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
                'co_inscripciones_cursadas' => array('clase'=>'co_inscripciones_cursadas','path'=>'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
                'co_inscriptos' => array('clase'=>'co_inscriptos','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
                'co_mesas_de_examen' => array('clase'=>'co_mesas_de_examen','path'=>'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
               'co_preinscripciones' => array('clase'=>'co_preinscripciones','path'=>'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
                'co_requisitos_ingreso' => array('clase'=>'co_requisitos_ingreso','path'=>'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
                'co_usuarios' => array('clase'=>'co_usuarios_pers','path'=>'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
        );

A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/asistencia/listado_asistencias
    
    class ci_rep_ctrl_inasistencia extends ci_reporte
    {
       /*protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';

       //Componente Visual de Informaci▒n
       protected $ev_info;

       protected $s__xcuadro;

       function get_tabla_principal()
       {
               return 'sga_alumnos';
       }

       function get_datos($filtro)
       {
               return toba::consulta_php('co_inasistencias')->get_listado($filtro);
       }



       function conf__cuadro(toba_ei_cuadro $cuadro)
       {
               if (isset($this->s__datos)) {
                       $datos = $this->get_datos($this->s__filtro);
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               }  else {
                       $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
               }
               $cuadro->set_filtro_asociado($this->dep('filtro'));
       }

       //---- filtro -----------------------------------------------------------------------

       function conf__filtro(toba_ei_filtro $filtro)
       {


       }*/

       protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
       protected $s__filtro_estado;
       protected $s__filtro_estado_rechazadas;

       //--------------------------------------------------------------------------
       //---- filtro --------------------------------------------------------------
       //--------------------------------------------------------------------------

       function conf__filtro(toba_ei_filtro $filtro)
       {
               parent::conf__filtro($filtro);
               $filtro->columna('nombre_alumno')->set_condicion_fija('contiene');
               $filtro->columna('anio_academico')->set_condicion_fija('es_igual_a');
               $filtro->columna('periodo_lectivo')->set_condicion_fija('es_igual_a');
       }

       /**
               * Redefinici▒n del evento filtrar, para que arme una cadena WHERE acorde con la
               * nueva estructura de modalidades de cursada de comisi▒n.
               */
       function evt__filtro__filtrar($datos)
       {
               if (isset($datos)) {
                       $this->s__datos = $datos;

                       $this->s__filtro = "{$this->dep('filtro')->get_sql_where()} $filtro";
               } else {
                       unset($this->s__datos);
                       $this->s__filtro = '';
               }
               /*echo '<pre style="font-size:16px">';
               var_dump($this->s__filtro);*/
       }

       function conf__cuadro(toba_ei_cuadro $cuadro)
       {
               if (isset($this->s__datos)) {
                       $datos = $this->get_datos($this->s__filtro);
                       $cuadro->set_datos($datos);
                       $cuadro->set_eof_mensaje($this->get_msg_eof());
               } else {
                       $cuadro->set_eof_mensaje(guarani_mensajes::get($this->msg_eof_cuadro));
               }
               $cuadro->set_filtro_asociado($this->dep('filtro'));
       }

       function get_tabla_principal()
       {
               //return 'sga_insc_cursada';
       }

       function get_datos($filtro)
       {
               /*echo '<pre style="font-size:16px">';
               $a = $this->dep('filtro');
               var_dump($a);
               $a->_columnas;*/
               return toba::consulta_php('co_ctrl_inasistencias')->get_listado($filtro, $this->s__datos);
       }
<br></br>
##### `r32688` 
- _Comandos ejecutados nuevamente._

<br></br>
##### **r34459 | dcelestino | 2019-08-05 11:01:07 -0300 (Mon, 05 Aug 2019)** 
- _Personalizaciones._

<br></br>
    
    ' as firma,
            sga_clases.clase,
            sga_asignaciones.dia_semana AS dia_semana,
            sga_clases.fecha AS fecha_clase,
            to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
            sga_clases.fecha,
            to_char(
                    sga_asignaciones.hora_inicio,
<br></br>
##### `r34509` 
- _Se sube archivos co_clases_diarias._

<br></br>
##### `r34973` 
- _Personalización de reporte de constancia de alumno regular._

<br></br>
##### **r38261 | dcelestino | 2020-02-04 12:34:49 -0300 (Tue, 04 Feb 2020)**
- _Campos nuevos al reporte de preinscritos._

<br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml
    
        <property name="ireport.zoom" value="1.0"/>
        <property name="ireport.x" value="0"/>
        <property name="ireport.y" value="0"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
        <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
        <parameter name="solicitud" class="java.lang.Integer">
        <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
        <parameter name="verificacion_qr" class="java.lang.String"/>
        <queryString>
                <![CDATA[SELECT
       COALESCE(sga_alumnos.legajo, ' -- ') AS legajo,
       vw_personas.apellido || ' ' || vw_personas.nombres as apellido_y_nombre,
       vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento as documento_principal,
       sga_propuestas.nombre as propuesta_nombre,
       '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre as propuesta_nombre_completo,
       sga_propuestas.nombre_abreviado as propuesta_nombre_abreviado,
       sga_ubicaciones.nombre as ubicacion_nombre,
       sga_planes.nombre as plan_nombre,
       sga_planes_versiones.nombre as plan_version_nombre,
       COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
       vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
       vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
       sga_propuestas.nombre AS propuesta_nombre,
       '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
       sga_propuestas.nombre_abreviado AS propuesta_nombre_abreviado,
       sga_ubicaciones.nombre AS ubicacion_nombre,
       sga_planes.nombre AS plan_nombre,
       sga_planes_versiones.nombre AS plan_version_nombre,
        sga_constancias_solicitud.presentar_a,
       COALESCE(sga_constancias_solicitud.observaciones, ' ') AS observaciones,
       vw_localidades.localidad_nombre as ciudad,
       vw_localidades.provincia_nombre as provincia,
       sga_instituciones.nombre as nombre_institucion
       COALESCE (
               sga_constancias_solicitud.observaciones,
               ' '
       ) AS observaciones,
       vw_localidades.localidad_nombre AS ciudad,
       vw_localidades.provincia_nombre AS provincia,
       sga_instituciones.nombre AS nombre_institucion,

       sga_alumnos.alumno,
       ARRAY_TO_STRING(ARRAY_AGG (
               sga_asignaciones.dia_semana || ' de ' ||  sga_asignaciones.hora_inicio || ' a ' || sga_asignaciones.hora_finalizacion || ' '
      ), ';') as Horarios
    FROM
       sga_constancias_solicitud,
       sga_alumnos,
        sga_planes,
       sga_instituciones,
       par_configuraciones,
      vw_localidades
       vw_localidades,
       sga_insc_cursada,
       sga_comisiones,
       sga_comisiones_bh,
       sga_asignaciones,
       sga_periodos_lectivos
       --,sga_clases_asistencia_acum
    WHERE
       sga_constancias_solicitud.solicitud = $P{solicitud}
       AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
       AND sga_alumnos.persona = vw_personas.persona
       AND sga_alumnos.calidad = 'A'
       AND sga_propuestas.propuesta = sga_alumnos.propuesta
       AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
       AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
       AND sga_planes.plan = sga_planes_versiones.plan
       AND par_configuraciones.nombre = 'institucion_instalacion'
       AND (par_configuraciones.valor::INTEGER) = sga_instituciones.institucion
       AND sga_ubicaciones.localidad = vw_localidades.localidad
       AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
       AND sga_alumnos.persona = vw_personas.persona
       AND sga_alumnos.calidad = 'A'
       AND sga_propuestas.propuesta = sga_alumnos.propuesta
       AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
       +AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
       AND sga_planes.plan = sga_planes_versiones.plan
       AND par_configuraciones.nombre = 'institucion_instalacion'
       AND (
              par_configuraciones.valor :: INTEGER
       ) = sga_instituciones.institucion
       AND sga_ubicaciones.localidad = vw_localidades.localidad
       AND sga_insc_cursada.alumno = sga_alumnos.alumno
       AND sga_insc_cursada.comision = sga_comisiones.comision
       AND sga_comisiones_bh.comision = sga_comisiones.comision
       AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
       AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
       AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
       AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
       /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
       AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
       AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
     GROUP BY
       sga_alumnos.legajo,
       vw_personas.apellido,
       vw_personas.nombres,
       vw_personas.desc_tipo_documento,
       sga_propuestas.nombre,
       sga_propuestas.codigo,
       vw_personas.nro_documento,
       sga_propuestas.nombre_abreviado,
       sga_ubicaciones.nombre,
       sga_planes.nombre,
       sga_planes_versiones.nombre,
       sga_constancias_solicitud.presentar_a,
       sga_constancias_solicitud.observaciones,
       vw_localidades.localidad_nombre,
       vw_localidades.provincia_nombre,
       sga_instituciones.nombre,
       sga_alumnos.alumno
              LIMIT 1;]]>
       </queryString>
       <field name="legajo" class="java.lang.String">
       <field name="nombre_institucion" class="java.lang.String">
               <fieldDescription><![CDATA[]]></fieldDescription>
       </field>
       <field name="horarios" class="java.lang.String"/>
       <variable name="fecha_narrada" class="java.lang.String">
               <variableExpression><![CDATA[new java.text.SimpleDateFormat("dd 'días del mes de' MMMM 'de' yyyy", new java.util.Locale("es")).format(new java.util.Date())]]></variableExpression>
       </variable>
       <background>
               <band height="546" splitType="Stretch">
                       <rectangle>
                               <reportElement positionType="Float" x="0" y="0" width="555" height="512" uuid="02a6fe6d-f633-49df-802a-8fb70f32f883"/>
                               <graphicElement>
                                       <pen lineWidth="1.5"/>
                               </graphicElement>
                       </rectangle>
               </band>
               <band height="546" splitType="Stretch"/>
       </background>
       <title>
               <band height="48" splitType="Stretch">
               <band splitType="Stretch"/>
       </columnHeader>
        <detail>
               <band height="366" splitType="Stretch">
               <band height="653" splitType="Stretch">
                      <textField isBlankWhenNull="true">
                               <reportElement x="53" y="13" width="447" height="91" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                              <textElement textAlignment="Justified"/>
                               <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + " " + $F{plan_version_nombre} + ", legajo Nro: " +  $F{legajo} + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", " + $F{provincia} + " a los " + $V{fecha_narrada} +"."]]></textFieldExpression>
                               <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                               <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                      </textField>
                       <staticText>
                              <reportElement x="131" y="251" width="29" height="20" uuid="87c75f57-6fcc-4e6f-98dc-cfae9a55c04b">
                                       <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                             </reportElement>
                               <text><![CDATA[Sello]]></text>
                      </staticText>
                      <line>
                               <reportElement x="330" y="250" width="130" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                               <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                       <line>
                               <reportElement x="83" y="250" width="130" height="1" uuid="e3e8256a-112d-4af9-bd3b-6c86288bd45b">
                                       <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                               </reportElement>
                       </line>
                       <textField isBlankWhenNull="true">
                               <reportElement x="53" y="114" width="447" height="76" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                               <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                               <reportElement x="264" y="251" width="261" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                               <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                               <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                               <reportElement x="264" y="271" width="261" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                               <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                               <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                        </textField>
                        <textField>
                               <reportElement x="125" y="298" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                               <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                        </textField>
                        <image>
                               <reportElement x="213" y="199" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                               <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                        </image>
                        <textField>
                               <reportElement x="83" y="318" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                               <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                        </textField>
                       <staticText>
                               <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                               <text><![CDATA[IUSE]]></text>
                       </staticText>
                       <image>
                               <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                               <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                       </image>
               </band>
        </detail>
        <columnFooter>

A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php
    
    $datos[$key]['turno_cursada'] = $dato['turno_cursada'];
                        $datos[$key]['e_mail'] = $dato['e_mail'];
                        $datos[$key]['celular_numero'] = $dato['celular_numero'];
                       $datos[$key]['iuse_pertenece_fuerzas_seguridad'] = $dato['iuse_pertenece_fuerzas_seguridad'];
                }
                return rs_ordenar_por_columnas($datos, array('responsable_academica', 'propuesta', 'apellido', 'nombres'));
        }

        protected function get_datos_reporte_desde_3w($condiciones, $origen)
        {

                $where = ' WHERE ';
                $where .= (!empty($condiciones['where_3w'])) ? $condiciones['where_3w'] : ' 1 = 1 ';

                                                AND mdp_personas_documentos.persona = mdp_personas.persona
                                        JOIN sga_preinscripcion_propuesta ON
                                                sga_preinscripcion_propuesta.persona = mdp_personas.persona

                                $where"";

                return guarani::db()->consultar($sql);
        }

                                        sga_preinscripcion_propuestas.fecha_preinscripcion,
                                        sga_preinscripcion_propuestas.fecha_fin_vigencia,
                                        sga_preinscripcion_propuestas.estado,

                                       CASE
                                               WHEN sga_preinscripcion.iuse_pertenece_fuerzas_seguridad = 1 THEN 'Si'
                                               ELSE 'No'
                                       END as pertenece_fuerzas,
                                       iuse_fuerzas.nombre as fuerza_nombre,
                                        CASE
                                                WHEN sga_preinscripcion_propuestas.estado = '" . preinscripcion::insc_procesada . "' THEN 'S▒'
                                                ELSE 'No'
                                        sga_preinscripcion
                                        JOIN sga_preinscripcion_propuestas ON
                                                sga_preinscripcion.id_preinscripcion = sga_preinscripcion_propuestas.id_preinscripcion
                                       LEFT JOIN iuse_fuerzas ON sga_preinscripcion.iuse_fuerza_descripcion = iuse_fuerzas.id
                                WHERE
                                        -- Se excluyen las Preinscripciones copiadas a G3 (se obtienen con el listado de 3w)
                                        sga_preinscripcion_propuestas.estado <> '" . preinscripcion::insc_copiada_g3 . "'
<br></br>
##### `r39707` 
- _Se agregó metodo para autenticar usuarios con web service._

<br></br>
##### **r39912 | dcelestino | 2020-05-04 14:42:23 -0300 (Mon, 04 May 2020)**
- _Restricción en elección de clave._

<br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml
     
    <?xml version="1.0" encoding="UTF-8"?>
    <jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd" name="guarani" pageWidth="595" pageHeight="842" whenNoDataType="NoDataSection" columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20" uuid="3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8">
           <property name="ireport.zoom" value="1.0"/>
       <property name="ireport.x" value="0"/>
       <property name="ireport.y" value="0"/>
       <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
       <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
       <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
       <parameter name="solicitud" class="java.lang.Integer">
               <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
       </parameter>
       <parameter name="logo" class="java.lang.String"/>
       <parameter name="autoridad_cargo" class="java.lang.String">
               <defaultValueExpression><![CDATA[""]]></defaultValueExpression>
       </parameter>
       <parameter name="autoridad_nombre" class="java.lang.String">
               <defaultValueExpression><![CDATA["Firma"]]></defaultValueExpression>
       </parameter>
       <parameter name="ocultar_firma" class="java.lang.Boolean">
               <defaultValueExpression><![CDATA[false]]></defaultValueExpression>
       </parameter>
       <parameter name="verificacion_codigo" class="java.lang.String"/>
       <parameter name="verificacion_url" class="java.lang.String"/>
       <parameter name="verificacion_qr" class="java.lang.String"/>
       <queryString>
               <![CDATA[SELECT
       COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
       vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
       vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
       sga_propuestas.nombre AS propuesta_nombre,
       '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
       sga_propuestas.nombre_abreviado AS propuesta_nombre_abreviado,
       sga_ubicaciones.nombre AS ubicacion_nombre,
       sga_planes.nombre AS plan_nombre,
       sga_planes_versiones.nombre AS plan_version_nombre,
       sga_constancias_solicitud.presentar_a,
       COALESCE (
               sga_constancias_solicitud.observaciones,
               ' '
       ) AS observaciones,
       vw_localidades.localidad_nombre AS ciudad,
       vw_localidades.provincia_nombre AS provincia,
       sga_instituciones.nombre AS nombre_institucion,

       sga_alumnos.alumno,
       ARRAY_TO_STRING(ARRAY_AGG (
               sga_asignaciones.dia_semana || ' de ' ||  sga_asignaciones.hora_inicio || ' a ' || sga_asignaciones.hora_finalizacion || ' '
       ), ';') as Horarios
    
     FROM
         sga_constancias_solicitud,
       sga_alumnos,
       vw_personas,
       sga_propuestas,
       sga_planes_versiones,
       sga_ubicaciones,
       sga_planes,
       sga_instituciones,
       par_configuraciones,
       vw_localidades,
       sga_insc_cursada,
       sga_comisiones,
       sga_comisiones_bh,
       sga_asignaciones,
       sga_periodos_lectivos
      --,sga_clases_asistencia_acum
    WHERE
        sga_constancias_solicitud.solicitud = $P{solicitud}
        AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
     AND sga_alumnos.persona = vw_personas.persona
     AND sga_alumnos.calidad = 'A'
     AND sga_propuestas.propuesta = sga_alumnos.propuesta
     AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
     AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
     ND sga_planes.plan = sga_planes_versiones.plan
     AND par_configuraciones.nombre = 'institucion_instalacion'
     AND (
            par_configuraciones.valor :: INTEGER
     ) = sga_instituciones.institucion
     AND sga_ubicaciones.localidad = vw_localidades.localidad
     AND sga_insc_cursada.alumno = sga_alumnos.alumno
     AND sga_insc_cursada.comision = sga_comisiones.comision
     AND sga_comisiones_bh.comision = sga_comisiones.comision
     AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
     AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
     AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
     AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
     /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
     AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
     +AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
    GROUP BY
        sga_alumnos.legajo,
        vw_personas.apellido,
        vw_personas.nombres,
        vw_personas.desc_tipo_documento,
        sga_propuestas.nombre,
        sga_propuestas.codigo,
        vw_personas.nro_documento,
        sga_propuestas.nombre_abreviado,
        sga_ubicaciones.nombre,
        sga_planes.nombre,
        sga_planes_versiones.nombre,
        sga_constancias_solicitud.presentar_a,
        sga_constancias_solicitud.observaciones,
        vw_localidades.localidad_nombre,
        vw_localidades.provincia_nombre,
        sga_instituciones.nombre,
        sga_alumnos.alumno
     LIMIT 1;]]>
           </queryString>
           <field name="legajo" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="apellido_y_nombre" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="documento_principal" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="propuesta_nombre" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="propuesta_nombre_completo" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="propuesta_nombre_abreviado" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="ubicacion_nombre" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="plan_nombre" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="plan_version_nombre" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="presentar_a" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="observaciones" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="ciudad" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="provincia" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="nombre_institucion" class="java.lang.String">
                   <fieldDescription><![CDATA[]]></fieldDescription>
           </field>
           <field name="horarios" class="java.lang.String"/>
           <variable name="fecha_narrada" class="java.lang.String">
                   <variableExpression><![CDATA[new java.text.SimpleDateFormat("dd 'días del mes de' MMMM 'de' yyyy", new java.util.Locale("es")).format(new java.util.Date())]]></variableExpression>
           </variable>
           <background>
                   <band height="546" splitType="Stretch"/>
           </background>
           <title>
                   <band height="48" splitType="Stretch">
                           <staticText>
                                   <reportElement style="Title" x="185" y="12" width="328" height="23" uuid="ee936c70-4673-4302-b64f-af7d7fead711"/>
                                   <text><![CDATA[Constancia de Alumno Regular]]></text>
                           </staticText>
                           <image>
                                   <reportElement x="42" y="5" width="92" height="40" uuid="9749d392-5fc0-48de-98e6-37ab50f757a3"/>
                                   <imageExpression><![CDATA[$P{logo}]]></imageExpression>
                           </image>
                   </band>
           </title>
           <pageHeader>
                   <band splitType="Stretch"/>
           </pageHeader>
           <columnHeader>
                   <band splitType="Stretch"/>
           </columnHeader>
           <detail>
                   <band height="653" splitType="Stretch">
                           <textField isBlankWhenNull="true">
                                   <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                   <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                           </textField>
                           <line>
                                   <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                           <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                   </reportElement>
                           </line>
                           <textField isBlankWhenNull="true">
                                   <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                           <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                           </textField>
                           <textField isBlankWhenNull="true">
                                   <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                           <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                   </reportElement>
                                   <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                           </textField>
                           <textField isBlankWhenNull="true">
                                   <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                           <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                   </reportElement>
                                   <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                           </textField>
                           <textField>
                                   <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                           <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                   </reportElement>
                                   <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                           </textField>
                           <image>
                                   <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                           <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                   </reportElement>
                                   <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                           </image>
                           <textField>
                                   <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                           <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                   </reportElement>
                                   <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                           </textField>
                           <staticText>
                                   <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                   <text><![CDATA[IUSE]]></text>
                           </staticText>
                           <image>
                                   <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                                   <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                          </image>
                   </band>
           </detail>
           <columnFooter>
               <band splitType="Stretch"/>
           </columnFooter> 
           <pageFooter>
               <band splitType="Stretch"/>
           </pageFooter>
           <summary>
               <band splitType="Stretch"/>
           </summary>
    </jasperReport>

M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/_lib/usuarios/usuario.php
class usuario extends usuario_nucleo {

    static function validar_clave_permitida($clave)
    {
               // Se controla la longitud mínima de la contraseña.
               // Se realiza el pedido anulando el uso de caché, debido a que este parámetro a nivel Institución
               // es consumido también desde Autogestión
               $longitud_minima = guarani::parametros()->get_valor('login_clave_longitud_minima', null, false);
               //permitimos solo letras y/o numeros en la clave
               $patron_valido =  (preg_match ("/^[a-zA-Z0-9]+$/", $clave)) ? true : false;
               return ((strlen($clave) >= $longitud_minima) && $patron_valido);
       }
     }
<br></br>
##### `r48082` 
- _Filtros "pertenece a fuerzas de seguridad"  en reporte de preinscritos._

<br></br>
##### **r48509 | dcelestino | 2021-03-12 12:56:33 -0300 (Fri, 12 Mar 2021)**
- _Se agregó campo mail al reporte de inscripción a propuestas._

<br></br>
M/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/co_inscripciones.php
    
    */
            function get_inscriptos_perfil_de_datos($where = '')
            {
    
                   /*$condiciones = explode('AND', $where);
                   $condicion = explode('=', $condiciones[0]);
                   $anio = $condicion[1];*/
                   $sql = "SELECT  nro_documento,
                                           CASE
                                                   WHEN sga_preinscripcion.iuse_pertenece_fuerzas_seguridad = 1 THEN 'Si'
                                                   WHEN sga_preinscripcion.iuse_pertenece_fuerzas_seguridad = 0 THEN 'No'
                                                   ELSE ''
                                           END as pertenece_fuerzas,
                                           sga_preinscripcion.iuse_grado_en_fuerza,
                                           iuse_fuerzas.nombre as fuerza_nombre,
                                           iuse_otras_policias_provinciales,
                                           iuse_grado_en_fuerza,
                                           iuse_antiguedad_general_fuerza
                                   FROM sga_preinscripcion
                                   LEFT JOIN iuse_fuerzas ON iuse_fuerzas.id = sga_preinscripcion.iuse_fuerza_descripcion";
                   $datos_preinscripcion = toba::db('preinscripcion')->consultar($sql);
                   //echo '<h1><br /><br />';
                   //var_dump($datos_preinscripcion[0][0]);
                   //die();
                   // $key = array_search('31210111', array_column($datos_preinscripcion, 'nro_documento'));
    
    
                    if ($where) {
                            $where = "WHERE $where";
                    }
                    $sql = "SELECT

                                                            array_to_string( ARRAY_AGG ( sga_comisiones.comision ), ', ') AS comisiones,
                                                            array_to_string( ARRAY_AGG (sga_comisiones.turno), ', ') AS turnos,
    
    
                                                            vw_personas.apellido_nombres,
                                                            vw_personas.tipo_nro_documento,
                                                           vw_personas.nro_documento,
                                 vw_personas.persona,
                                                            sga_alumnos.propuesta,
                                                            vw_perfil_de_datos_propuestas.propuesta_descripcion,
    
                                                            vw_perfil_de_datos_propuestas.nombre,
                                                            vw_personas.apellido,
                                                            vw_personas.nombres,
                                                            mdp_personas_contactos.email
                                                            mdp_personas_contactos.email,

                                                            vw_personas.nro_documento

                                    ORDER BY
                                                            vw_perfil_de_datos_propuestas.nombre,
                                                            vw_personas.apellido,
                                                            vw_personas.nombres
                    ";
                   return guarani_db::consultar($sql);

                   $datos_gestion = guarani_db::consultar($sql);
                   /*
                   iuse_pertenece_fuerzas_seguridad,
                                                  iuse_fuerza_descripcion,
                                                   iuse_otras_policias_provinciales,
                                                   iuse_grado_en_fuerza,
                                                   iuse_antiguedad_general_fuerza
                   */
                   foreach($datos_gestion as $k => $v){
                           $nro_documento = $v['nro_documento'];
                           if ($key = array_search($nro_documento, array_column($datos_preinscripcion, 'nro_documento'))){
                                   //$datos_gestion[$k]
                                   $datos[] = array_merge($datos_gestion[$k], $datos_preinscripcion[$key]);
                           }    
                           else{
                                   $datos[] = $datos_gestion[$k];
                           }
                   }

                   # return guarani_db::consultar($sql);
                   return $datos;
            }
    /**
<br></br>
##### **r48703 | dcelestino | 2021-03-25 14:12:28 -0300 (Thu, 25 Mar 2021)**
- _Se agregaron campos al reporte de inscripcion a propuestas. "pertenece o no" a fuerzas policiales._

<br></br>
M/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/co_inscripciones.php
    
    WHEN sga_preinscripcion.iuse_pertenece_fuerzas_seguridad = 0 THEN 'No'
                                                    ELSE ''
                                            END as pertenece_fuerzas,
                                            sga_preinscripcion.iuse_grado_en_fuerza,
                                            iuse_fuerzas.nombre as fuerza_nombre,
                                            iuse_otras_policias_provinciales,
                                            iuse_grado_en_fuerza,

<br></br>
##### `r53949` 
- _Se agregó una coma luego del apellido del alumno._

 <br></br>
##### `r54795` 
- _Se agrega campo nuevo al reporte de inscriptos por propuestas._

 <br></br>
##### **r55537 | dcelestino | 2021-10-18 11:24:10 -0300 (Mon, 18 Oct 2021)**
- _Se corrige constancia alumno regular, se cortaba el texto que indica los horarios del alumno._

<br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml
    
    <property name="ireport.zoom" value="1.0"/>
        <property name="ireport.x" value="0"/>
        <property name="ireport.y" value="0"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
        <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
        <parameter name="solicitud" class="java.lang.Integer">
                <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
        <parameter name="verificacion_qr" class="java.lang.String"/>
        <queryString>
                <![CDATA[SELECT
        COALESCE(sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ', ' || vw_personas.nombres as apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento as documento_principal,
        sga_propuestas.nombre as propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre as propuesta_nombre_completo,
        sga_propuestas.nombre_abreviado as propuesta_nombre_abreviado,
        sga_ubicaciones.nombre as ubicacion_nombre,
        sga_planes.nombre as plan_nombre,
        sga_planes_versiones.nombre as plan_version_nombre,
        COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
        sga_propuestas.nombre AS propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
        sga_propuestas.nombre_abreviado AS propuesta_nombre_abreviado,
        sga_ubicaciones.nombre AS ubicacion_nombre,
        sga_planes.nombre AS plan_nombre,
        sga_planes_versiones.nombre AS plan_version_nombre,
        sga_constancias_solicitud.presentar_a,
        COALESCE(sga_constancias_solicitud.observaciones, ' ') AS observaciones,
        vw_localidades.localidad_nombre as ciudad,
        vw_localidades.provincia_nombre as provincia,
        sga_instituciones.nombre as nombre_institucion
        COALESCE (
                sga_constancias_solicitud.observaciones,
                ' '
        ) AS observaciones,
        vw_localidades.localidad_nombre AS ciudad,
        vw_localidades.provincia_nombre AS provincia,
        sga_instituciones.nombre AS nombre_institucion,
 
        sga_alumnos.alumno,
        ARRAY_TO_STRING(ARRAY_AGG (
                sga_asignaciones.dia_semana || ' de ' ||  sga_asignaciones.hora_inicio || ' a ' || sga_asignaciones.hora_finalizacion || ' '
        ), ';') as Horarios
     FROM
        sga_constancias_solicitud,
        sga_alumnos,
        sga_planes,
        sga_instituciones,
        par_configuraciones,
        vw_localidades
        vw_localidades,
        sga_insc_cursada,
        sga_comisiones,
        sga_comisiones_bh,
        sga_asignaciones,
        sga_periodos_lectivos
        --,sga_clases_asistencia_acum
     WHERE
        sga_constancias_solicitud.solicitud = $P{solicitud}
        AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
        AND sga_alumnos.persona = vw_personas.persona
        AND sga_alumnos.calidad = 'A'
        AND sga_propuestas.propuesta = sga_alumnos.propuesta
        AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
        AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
        AND sga_planes.plan = sga_planes_versiones.plan
        AND par_configuraciones.nombre = 'institucion_instalacion'
        AND (par_configuraciones.valor::INTEGER) = sga_instituciones.institucion
        AND sga_ubicaciones.localidad = vw_localidades.localidad
        AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
        AND sga_alumnos.persona = vw_personas.persona
        AND sga_alumnos.calidad = 'A'
        AND sga_propuestas.propuesta = sga_alumnos.propuesta
        AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
        AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
        AND sga_planes.plan = sga_planes_versiones.plan
        AND par_configuraciones.nombre = 'institucion_instalacion'
        AND (
               par_configuraciones.valor :: INTEGER
        ) = sga_instituciones.institucion
        AND sga_ubicaciones.localidad = vw_localidades.localidad
        AND sga_insc_cursada.alumno = sga_alumnos.alumno
        AND sga_insc_cursada.comision = sga_comisiones.comision
        AND sga_comisiones_bh.comision = sga_comisiones.comision
        AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
        AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
        AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
        AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
        /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
        AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
        AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
       GROUP BY
               sga_alumnos.legajo,
               vw_personas.apellido,
               vw_personas.nombres,
               vw_personas.desc_tipo_documento,
               sga_propuestas.nombre,
               sga_propuestas.codigo,
               vw_personas.nro_documento,
               sga_propuestas.nombre_abreviado,
               sga_ubicaciones.nombre,
               sga_planes.nombre,
               sga_planes_versiones.nombre,
               sga_constancias_solicitud.presentar_a,
               sga_constancias_solicitud.observaciones,
               vw_localidades.localidad_nombre,
               vw_localidades.provincia_nombre,
               sga_instituciones.nombre,
               sga_alumnos.alumno
         LIMIT 1;]]>
                </queryString>
                <field name="legajo" class="java.lang.String">
 
                <field name="nombre_institucion" class="java.lang.String">
                <fieldDescription><![CDATA[]]></fieldDescription>
                </field>
                <field name="horarios" class="java.lang.String"/>
                <variable name="fecha_narrada" class="java.lang.String">
                <variableExpression><![CDATA[new java.text.SimpleDateFormat("dd 'días del mes de' MMMM 'de' yyyy", new java.util.Locale("es")).format(new java.util.Date())]]></variableExpression>
                </variable>
        <background>
               <band height="546" splitType="Stretch">
                        <rectangle>
                                <reportElement positionType="Float" x="0" y="0" width="555" height="512" uuid="02a6fe6d-f633-49df-802a-8fb70f32f883"/>
                                <graphicElement>
                                       <pen lineWidth="1.5"/>
                                </graphicElement>
                        </rectangle>
                </band>
                       <band height="546" splitType="Stretch"/>
        </background>
        <title>
                <band height="48" splitType="Stretch">
                <band splitType="Stretch"/>
        </columnHeader>
        <detail>
                <band height="366" splitType="Stretch">
                       <band height="653" splitType="Stretch">
                        <textField isBlankWhenNull="true">
                                <reportElement x="53" y="13" width="447" height="91" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                <textElement textAlignment="Justified"/>
                                <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + " " + $F{plan_version_nombre} + ", legajo Nro: " +  $F{legajo} + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", " + $F{provincia} + " a los " + $V{fecha_narrada} +"."]]></textFieldExpression>
                                <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                        </textField>
                               <staticText>
                                       <reportElement x="131" y="251" width="29" height="20" uuid="87c75f57-6fcc-4e6f-98dc-cfae9a55c04b">
                                               <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                       </reportElement>
                                       <text><![CDATA[Sello]]></text>
                               </staticText>
                        <line>
                                       <reportElement x="330" y="250" width="130" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                               <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                               <line>
                                <reportElement x="83" y="250" width="130" height="1" uuid="e3e8256a-112d-4af9-bd3b-6c86288bd45b">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                        <textField isBlankWhenNull="true">
                                <reportElement x="53" y="114" width="447" height="76" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="264" y="251" width="261" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                                <reportElement x="264" y="271" width="261" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                        </textField>
                        <textField>
                               <reportElement x="125" y="298" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                               <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                        </textField>
                        <image>
                                <reportElement x="213" y="199" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                        </image>
                        <textField>
                                <reportElement x="83" y="318" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                        </textField>
                        <staticText>
                                <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                <text><![CDATA[IUSE]]></text>
                        </staticText>
                        <image>
                                <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                                <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                        </image>
                </band>
        </detail>
        <columnFooter>
<br></br>
##### **r57038 | dcelestino | 2021-11-26 11:18:20 -0300 (Fri, 26 Nov 2021)**
- _Modificación de reporte de constancia de actividades aprobadas._

<br></br>
A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaActividadesAprobadas.jrxml
    
    <?xml version="1.0" encoding="UTF-8"?>
    <!-- Created with Jaspersoft Studio version 6.18.1.final using JasperReports Library version 6.18.1-9d75d1969e774d4f179fb3be8401e98a0e6d1611  -->
    <jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd" name="guarani" language="groovy" pageWidth="595" pageHeight="842" columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20" uuid="d025d606-8fcc-4325-a190-2fdb26fba675">
        <property name="ireport.zoom" value="1.4641000000000006"/>
        <property name="ireport.x" value="0"/>
                                                <connectionExpression><![CDATA[$P{REPORT_CONNECTION}]]></connectionExpression>
                                        </datasetRun>
                                        <jr:listContents height="19">
                                               <textField isStretchWithOverflow="true">
                                               <textField textAdjust="StretchHeight">
                                                        <reportElement style="Comun" stretchType="RelativeToTallestObject" x="19" y="0" width="160" height="18" uuid="d3842c1a-cdc9-440b-834e-8e983187215f"/>
                                                        <textFieldExpression><![CDATA[$F{actividad_descr}]]></textFieldExpression>
                                                </textField>
                                               <textField isStretchWithOverflow="true">
                                               <textField textAdjust="StretchHeight">
                                                        <reportElement style="Comun" x="179" y="1" width="69" height="17" uuid="8ae02570-e798-4bf0-bfe1-628920db5f81"/>
                                                        <textElement textAlignment="Center"/>
                                                        <textFieldExpression><![CDATA[$F{fecha}]]></textFieldExpression>
                                                </textField>
                                               <textField isStretchWithOverflow="true" isBlankWhenNull="true">
                                               <textField textAdjust="StretchHeight" isBlankWhenNull="true">
                                                        <reportElement style="Comun" x="248" y="1" width="69" height="17" uuid="b917354c-1a12-4b2f-9861-716d6af8bdca"/>
                                                        <textElement textAlignment="Center"/>
                                                        <textFieldExpression><![CDATA[$F{nota_completa}]]></textFieldExpression>
                                                </textField>
                                               <textField isStretchWithOverflow="true">
                                               <textField textAdjust="StretchHeight">
                                                        <reportElement style="Comun" stretchType="RelativeToTallestObject" x="317" y="1" width="97" height="17" uuid="c07e2087-5858-4fd6-b10a-96dd26a11cef"/>
                                                        <textElement textAlignment="Center"/>
                                                        <textFieldExpression><![CDATA[$F{tipo}]]></textFieldExpression>
                                                </textField>
                                               <textField isStretchWithOverflow="true" isBlankWhenNull="true">
                                               <textField textAdjust="StretchHeight" isBlankWhenNull="true">
                                                        <reportElement style="Comun" stretchType="RelativeToTallestObject" x="415" y="1" width="69" height="17" uuid="d1b69011-8b89-4193-8a8d-4bca5d64de03"/>
                                                        <textElement textAlignment="Center"/>
                                                        <textFieldExpression><![CDATA[$F{actividad_documento}]]></textFieldExpression>
                                                </textField>
                                               <textField isStretchWithOverflow="true" isBlankWhenNull="true">
                                               <textField textAdjust="StretchHeight" isBlankWhenNull="true">
                                                        <reportElement style="Comun" x="483" y="1" width="52" height="17" uuid="3d053b94-ee57-46d4-8db4-ba0db7ca9198"/>
                                                        <textElement textAlignment="Center"/>
                                                        <textFieldExpression><![CDATA[$F{folio_fisico}]]></textFieldExpression>
        <summary>
                <band height="314" splitType="Stretch">
                        <textField isBlankWhenNull="true">
                               <reportElement style="Comun" x="287" y="185" width="206" height="20" uuid="1a4d4b61-9022-4648-8cc1-8c72e5672e55">
                               <reportElement style="Comun" x="190" y="182" width="206" height="20" uuid="1a4d4b61-9022-4648-8cc1-8c72e5672e55">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Top">
                                <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                        </textField>
                        <textField isBlankWhenNull="true">
                               <reportElement style="Comun" x="287" y="205" width="206" height="20" uuid="a94115c7-72d5-45a9-9758-31a1ba8fdfa3">
                               <reportElement style="Comun" x="190" y="202" width="206" height="20" uuid="a94115c7-72d5-45a9-9758-31a1ba8fdfa3">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                                <textElement textAlignment="Center" verticalAlignment="Top">
                                <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                        </textField>
                        <line>
                               <reportElement x="325" y="183" width="130" height="1" forecolor="#000000" uuid="8d93bf9d-4873-4ab3-bc3d-cdc8def1ab07">
                               <reportElement x="217" y="180" width="130" height="1" forecolor="#000000" uuid="8d93bf9d-4873-4ab3-bc3d-cdc8def1ab07">
                                        <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                </reportElement>
                        </line>
                       <staticText>
                               <reportElement style="Resalt" x="105" y="185" width="29" height="20" uuid="6927d449-1c9f-453a-9767-fac06693f137">
                                       <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                               </reportElement>
                               <textElement textAlignment="Center">
                                       <font isBold="false" pdfFontName="Helvetica"/>
                               </textElement>
                               <text><![CDATA[Sello]]></text>
                       </staticText>
                       <line>
                               <reportElement x="54" y="184" width="130" height="1" uuid="6d471a23-4fe1-4a9d-a764-020ae862d947">
                                       <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                               </reportElement>
                       </line>
                        <textField>
                                <reportElement style="Comun" x="48" y="64" width="447" height="41" uuid="86bc625f-82b7-4b7c-8c63-18cc52d350be"/>
                                <textElement textAlignment="Justified">
                                <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                        </textField>
                        <image>
                               <reportElement x="222" y="113" width="92" height="92" uuid="d251c01a-f333-4709-b450-9c7314283418">
                               <reportElement x="42" y="110" width="92" height="92" uuid="d251c01a-f333-4709-b450-9c7314283418">
                                        <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                </reportElement>
                                <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
<br></br>

##### **r59597 | dcelestino | 2022-04-11 11:04:37 -0300 (Mon, 11 Apr 2022)**
- _se agrega firma de nessi añl reporte de constancia de materias aprobadas._
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaActividadesAprobadas.jrxml
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/www/img/firma_nessi_small.png

    
        <property name="ireport.zoom" value="1.0"/>
        <property name="ireport.x" value="0"/>
        <property name="ireport.y" value="0"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1" value="430"/>
        <property name="com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2" value="564"/>
        <style name="Title" fontName="Times New Roman" fontSize="14" isBold="true" isUnderline="true" pdfFontName="Times-Bold"/>
        <parameter name="solicitud" class="java.lang.Integer">
                <defaultValueExpression><![CDATA[new Integer(1)]]></defaultValueExpression>
        <parameter name="verificacion_qr" class="java.lang.String"/>
        <queryString>
                <![CDATA[SELECT
        COALESCE(sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ', ' || vw_personas.nombres as apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento as documento_principal,
        sga_propuestas.nombre as propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre as propuesta_nombre_completo,
        sga_propuestas.nombre_abreviado as propuesta_nombre_abreviado,
        sga_ubicaciones.nombre as ubicacion_nombre,
        sga_planes.nombre as plan_nombre,
        sga_planes_versiones.nombre as plan_version_nombre,
        COALESCE (sga_alumnos.legajo, ' -- ') AS legajo,
        vw_personas.apellido || ', ' || vw_personas.nombres AS apellido_y_nombre,
        vw_personas.desc_tipo_documento || ' ' || vw_personas.nro_documento AS documento_principal,
        sga_propuestas.nombre AS propuesta_nombre,
        '(' || sga_propuestas.codigo || ') ' || sga_propuestas.nombre AS propuesta_nombre_completo,
        sga_propuestas.nombre_abreviado AS propuesta_nombre_abreviado,
        sga_ubicaciones.nombre AS ubicacion_nombre,
        sga_planes.nombre AS plan_nombre,
        sga_planes_versiones.nombre AS plan_version_nombre,
        sga_constancias_solicitud.presentar_a,
        COALESCE(sga_constancias_solicitud.observaciones, ' ') AS observaciones,
        vw_localidades.localidad_nombre as ciudad,
        vw_localidades.provincia_nombre as provincia,
        sga_instituciones.nombre as nombre_institucion
        COALESCE (
                sga_constancias_solicitud.observaciones,
                ' '
        ) AS observaciones,
        vw_localidades.localidad_nombre AS ciudad,
        vw_localidades.provincia_nombre AS provincia,
        sga_instituciones.nombre AS nombre_institucion,
        sga_alumnos.alumno,
        ARRAY_TO_STRING(ARRAY_AGG (
                sga_asignaciones.dia_semana || ' de ' ||  sga_asignaciones.hora_inicio || ' a ' || sga_asignaciones.hora_finalizacion || ' '
        ), ';') as Horarios
        FROM
         sga_constancias_solicitud,
         sga_alumnos,
         sga_planes,
         sga_instituciones,
         par_configuraciones,
         vw_localidades
         vw_localidades,
         sga_insc_cursada,
         sga_comisiones,
         sga_comisiones_bh,
         sga_asignaciones,
         sga_periodos_lectivos
         --,sga_clases_asistencia_acum
        WHERE
         sga_constancias_solicitud.solicitud = $P{solicitud}
         AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
         AND sga_alumnos.persona = vw_personas.persona
         AND sga_alumnos.calidad = 'A'
         AND sga_propuestas.propuesta = sga_alumnos.propuesta
         AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
         AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
         AND sga_planes.plan = sga_planes_versiones.plan
         AND par_configuraciones.nombre = 'institucion_instalacion'
         AND (par_configuraciones.valor::INTEGER) = sga_instituciones.institucion
         AND sga_ubicaciones.localidad = vw_localidades.localidad
         AND sga_constancias_solicitud.alumno = sga_alumnos.alumno
         AND sga_alumnos.persona = vw_personas.persona
         AND sga_alumnos.calidad = 'A'
         AND sga_propuestas.propuesta = sga_alumnos.propuesta
         AND sga_planes_versiones.plan_version = sga_alumnos.plan_version
         AND sga_alumnos.ubicacion = sga_ubicaciones.ubicacion
         AND sga_planes.plan = sga_planes_versiones.plan
         AND par_configuraciones.nombre = 'institucion_instalacion'
         AND (
                par_configuraciones.valor :: INTEGER
             ) = sga_instituciones.institucion
         AND sga_ubicaciones.localidad = vw_localidades.localidad
         AND sga_insc_cursada.alumno = sga_alumnos.alumno
         AND sga_insc_cursada.comision = sga_comisiones.comision
         AND sga_comisiones_bh.comision = sga_comisiones.comision
         AND sga_asignaciones.asignacion = sga_comisiones_bh.asignacion
         AND sga_periodos_lectivos.periodo_lectivo = sga_comisiones.periodo_lectivo
         AND sga_periodos_lectivos.fecha_inicio_dictado < NOW()::DATE
         AND sga_periodos_lectivos.fecha_fin_dictado > NOW()::DATE
         /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
         AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
         AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
        GROUP BY
         sga_alumnos.legajo,
         vw_personas.apellido,
         vw_personas.nombres,
         vw_personas.desc_tipo_documento,
         sga_propuestas.nombre,
         sga_propuestas.codigo,
         vw_personas.nro_documento,
         sga_propuestas.nombre_abreviado,
         sga_ubicaciones.nombre,
         sga_planes.nombre,
         sga_planes_versiones.nombre,
         sga_constancias_solicitud.presentar_a,
         sga_constancias_solicitud.observaciones,
         vw_localidades.localidad_nombre,
         vw_localidades.provincia_nombre,
         sga_instituciones.nombre,
         sga_alumnos.alumno
        LIMIT 1;]]>
         </queryString>
         <field name="legajo" class="java.lang.String">
         <field name="nombre_institucion" class="java.lang.String">
                 <fieldDescription><![CDATA[]]></fieldDescription>
         </field>
         <field name="horarios" class="java.lang.String"/>
         <variable name="fecha_narrada" class="java.lang.String">
                 <variableExpression><![CDATA[new java.text.SimpleDateFormat("dd 'días del mes de' MMMM 'de' yyyy", new java.util.Locale("es")).format(new java.util.Date())]]></variableExpression>
         </variable>
         <background>
                 <band height="546" splitType="Stretch">
                         <rectangle>
                                 <reportElement positionType="Float" x="0" y="0" width="555" height="512" uuid="02a6fe6d-f633-49df-802a-8fb70f32f883"/>
                                 <graphicElement>
                                         <pen lineWidth="1.5"/>
                                 </graphicElement>
                         </rectangle>
                 </band>
                 <band height="546" splitType="Stretch"/>
         </background>
         <title>
                 <band height="48" splitType="Stretch">
                 <band splitType="Stretch"/>
         </columnHeader>
         <detail>
                 <band height="366" splitType="Stretch">
                 <band height="653" splitType="Stretch">
                          <textField isBlankWhenNull="true">
                                 <reportElement x="53" y="13" width="447" height="91" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                 <textElement textAlignment="Justified"/>
                                 <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + " " + $F{plan_version_nombre} + ", legajo Nro: " +  $F{legajo} + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", " + $F{provincia} + " a los " + $V{fecha_narrada} +"."]]></textFieldExpression>
                                 <reportElement x="53" y="13" width="447" height="209" uuid="e716409d-f2dd-4889-a9b1-d6b9f1d7d764"/>
                                 <textFieldExpression><![CDATA["La sección alumnado de el/la " + $F{nombre_institucion} + " certifica que " + $F{apellido_y_nombre}.toUpperCase() + " con " + $F{documento_principal} + " está inscripto(/a) como alumno(/a) regular en la propuesta de " + $F{propuesta_nombre}.toUpperCase() + ". A su pedido y para su presentación ante " + $F{presentar_a}.toUpperCase() + " se le extiende la presente en " + $F{ciudad} + ", a los " + $V{fecha_narrada} +". \nHorarios: " + $F{horarios}]]></textFieldExpression>
                          </textField>
                          <staticText>
                                 <reportElement x="131" y="251" width="29" height="20" uuid="87c75f57-6fcc-4e6f-98dc-cfae9a55c04b">
                                         <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                 </reportElement>
                                 <text><![CDATA[Sello]]></text>
                         </staticText>
                         <line>
                                 <reportElement x="330" y="250" width="130" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                 <reportElement x="185" y="420" width="182" height="1" uuid="f8b38d59-8c6e-464a-be45-68347b7297a0">
                                         <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                 </reportElement>
                         </line>
                         <line>
                                 <reportElement x="83" y="250" width="130" height="1" uuid="e3e8256a-112d-4af9-bd3b-6c86288bd45b">
                                         <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                 </reportElement>
                         </line>
                         <textField isBlankWhenNull="true">
                                 <reportElement x="53" y="114" width="447" height="76" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                 <reportElement x="53" y="239" width="447" height="60" uuid="e418a161-258f-44f3-b39d-fe2ecdbd0057"/>
                                 <textFieldExpression><![CDATA[((($F{observaciones}.trim()).isEmpty()) ? "" : ("OBSERVACIONES: " + $F{observaciones}))]]></textFieldExpression>
                         </textField>
                         <textField isBlankWhenNull="true">
                                 <reportElement x="264" y="251" width="261" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                 <reportElement x="230" y="450" width="220" height="20" uuid="b5811651-8d92-48a8-b842-ec2224484307">
                                         <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                 </reportElement>
                                 <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                 <textFieldExpression><![CDATA[$P{autoridad_nombre}]]></textFieldExpression>
                         </textField>
                         <textField isBlankWhenNull="true">
                                 <reportElement x="264" y="271" width="261" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                 <reportElement x="220" y="432" width="258" height="20" uuid="a4589143-fb55-4d0b-9d67-591e08735960">
                                         <printWhenExpression><![CDATA[($P{ocultar_firma}.booleanValue() == false)]]></printWhenExpression>
                                 </reportElement>
                                 <textElement textAlignment="Center" verticalAlignment="Middle"/>
                                 <textFieldExpression><![CDATA[$P{autoridad_cargo}]]></textFieldExpression>
                         </textField>
                         <textField>
                                 <reportElement x="125" y="298" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                 <reportElement x="127" y="510" width="300" height="20" uuid="200650ae-706e-401d-acf0-2534b488e940">
                                         <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                 </reportElement>
                                 <textFieldExpression><![CDATA["CÓDIGO DE VALIDACIÓN: " + $P{verificacion_codigo}]]></textFieldExpression>
                         </textField>
                         <image>
                                 <reportElement x="213" y="199" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                 <reportElement x="230" y="289" width="92" height="92" uuid="62120307-e032-45a9-a72a-05e9469a2986">
                                         <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                 </reportElement>
                                 <imageExpression><![CDATA[$P{verificacion_qr}]]></imageExpression>
                         </image>
                         <textField>
                                 <reportElement x="83" y="318" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                 <reportElement x="76" y="560" width="417" height="48" uuid="5d811c69-acde-41c8-8f89-04c6cf482e6a">
                                         <printWhenExpression><![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]></printWhenExpression>
                                 </reportElement>
                                 <textFieldExpression><![CDATA["Este certificado podrá ser validado ingresando a " + $P{verificacion_url}+ " completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR."]]></textFieldExpression>
                         </textField>
                         <staticText>
                                 <reportElement x="250" y="470" width="128" height="20" uuid="53d8d55d-d87a-46da-a013-345ba8b7ee91"/>
                                 <text><![CDATA[IUSE]]></text>
                         </staticText>
                         <image>
                                 <reportElement x="222" y="313" width="100" height="97" uuid="590eee88-216f-427a-a99f-2d8504ffa57a"/>
                                 <imageExpression><![CDATA["/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png"]]></imageExpression>
                         </image>
                 </band>
         </detail>
         <columnFooter>
         Index: www/img/firma_nessi_small.png

<br></br>

##### **r59622 | dcelestino | 2022-04-12 10:37:20 -0300 (Tue, 12 Apr 2022)**

- _Se corrige firma en constancia de actividades aprobadas, y se agrega firma a reporte de constancia de alumno regular._

<br></br>

---
##Imágenes correspondientes al historial de actualizaciones
<br></br>


####Desarrollo de reporte nuevo de Clases Diarias 
![Screenshot que muestra el reporte de clases diarias.](http://drive.google.com/uc?export=view&id=1AlduaVhEuKBrGmrOaIerd8rWo3A6dShf "Desarrollo de reporte nuevo de Clases Diarias")

####Se modificó el reporte de Constancia de Alumno Regular
![Screenshot constancia de alumno regular.](http://drive.google.com/uc?export=view&id=1phzdNN2Wp6mBYRhas1xidxJ5KJ5EcX2m "Se modificó el reporte de Constancia de Alumno Regular ")

####Se desarrolló script para posicionar el cursor en el cuadro de búsqueda al clickear en el menú
![Screenshot mostrando el posicionamiento del cursor](http://drive.google.com/uc?export=view&id=1hHtHv1qrEtN3614VVw9txmvyJwh4Kvxx "Se desarrolló script para posicionar el cursor en el cuadro de búsqueda al clickear en el menú")

####Se agrego filtro por propuesta al reporte de mesas de exámenes 
![Screenshot mostrando el filtro agregado.](http://drive.google.com/uc?export=view&id=1VQXlpP5j0hKcuG52Z2kznXOqMNKHOKAM "Se agrego filtro por propuesta al reporte de mesas de exámenes")

####Se agrego el campo email al reporte de inscripciones a cursadas
![Screenshot señalando el campo agregado.](http://drive.google.com/uc?export=view&id=1ULJSGQAuU2mEkK8Zk-cvy2-Fr5uiDNfP "Se agrego el campo email al reporte de inscripciones a cursadas")

####Campos nuevos al reporte de preinscriptos 
![Screenshot recuadrando este reporte nuevo.](http://drive.google.com/uc?export=view&id=1BvDxeTPx_ToHQD-ZyLnydDMgE0Z0d7np "Desarrollo de reporte nuevo de Clases Diarias")

####Se desarrolló webservice para autenticarse 
![Servicio de webservice para autenticación.](http://drive.google.com/uc?export=view&id=1KIFPzPXpvUoqTWwycJEKgzYsTinvoeNG "Se desarrolló webservice para autenticarse ")

####Restricción en elección de clave al generar contraseña
![Screenshot mostrando los requisitos para llevar a cabo la generacón de contraseña](http://drive.google.com/uc?export=view&id=1Dloz4WiLlFEhB_6rzJtpIr7qBVkPrkWU "Restricción en elección de clave al generar contraseña")

####Filtros "pertenece a fuerzas de seguridad" en reporte de preinscritos  
![Screenshot señalando el filtro que denota lo indicado.](http://drive.google.com/uc?export=view&id=1vFJf-jUO24NgvzfAXwUf7zwIulP17OGR "Filtros "pertenece a fuerzas de seguridad" en reporte de preinscritos ")

####Se agregó campo mail al reporte de inscripción a propuestas
![Muestra del agregado del campo mail.](http://drive.google.com/uc?export=view&id=1-fqkbmZOcalfFTs8jCEXUQrpcdd8f7oq "Se agregó campo mail al reporte de inscripción a propuestas")