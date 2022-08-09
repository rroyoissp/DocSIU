<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body {
  font-family: "Lato", sans-serif;
}

/* Fixed sidenav, full height */
.sidenav {
  height: 100%;
  width: 200px;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  background-color: #111;
  overflow-x: hidden;
  padding-top: 20px;
}

/* Style the sidenav links and the dropdown button */
.sidenav a, .dropdown-btn {
  padding: 6px 8px 6px 16px;
  text-decoration: none;
  font-size: 15px;
  color: #818181;
  display: block;
  border: none;
  background: none;
  width: 100%;
  text-align: left;
  cursor: pointer;
  outline: none;
}

/* On mouse-over */
.sidenav a:hover, .dropdown-btn:hover {
  color: #f1f1f1;
}

/* Main content */
.main {
  margin-left: 200px; /* Same as the width of the sidenav */
  font-size: 20px; /* Increased text to enable scrolling */
  padding: 0px 10px;
}

/* Add an active class to the active dropdown button */
.active {
  background-color: green;
  color: white;
}

/* Dropdown container (hidden by default). Optional: add a lighter background color and some left padding to change the design of the dropdown content */
.dropdown-container {
  display: none;
  background-color: #262626;
  padding-left: 8px;
}

/* Optional: Style the caret down icon */
.fa-caret-down {
  float: right;
  padding-right: 8px;
}

/* Some media queries for responsiveness */
@media screen and (max-height: 450px) {
  .sidenav {padding-top: 15px;}
  .sidenav a {font-size: 18px;}
}
</style>
</head>
<body>

<div class="sidenav">
  <a href="#clients">Inicio</a>
  <a href="#contact">Sergio</a>
  <button class="dropdown-btn">DCelestino 
    <i class="fa fa-caret-down"></i>
  </button>
  <div class="dropdown-container">
    <a href="#">r30488</a>
    <a href="#">r31220</a>
    <a href="#">r31221</a>
    <a href="#">r31228</a>
    <a href="#">r31232</a>
    <a href="#">r31233</a>
    <a href="#">r31800</a>
    <a href="#">r31839</a>
    <a href="#">r32677</a>
    <a href="#">r34459</a>
    <a href="#">r38261</a>
    <a href="#">r39912</a>
    <a href="#">r48509</a>
    <a href="#">r48703</a>
    <a href="#">r55537</a>
    <a href="#">r57038</a>
    <a href="#">r59597</a>
    <a href="#">r59622</a>
  </div>
  <a href="#contact">Imágenes</a>
</div>

<script>
/* Loop through all dropdown buttons to toggle between hiding and showing its dropdown content - This allows the user to have multiple dropdowns without any conflict */
var dropdown = document.getElementsByClassName("dropdown-btn");
var i;

for (i = 0; i < dropdown.length; i++) {
  dropdown[i].addEventListener("click", function() {
  this.classList.toggle("active");
  var dropdownContent = this.nextElementSibling;
  if (dropdownContent.style.display === "block") {
  dropdownContent.style.display = "none";
  } else {
  dropdownContent.style.display = "block";
  }
  });
}
</script>


<div class="main">
  <h1>Documentación SIU IUSE - ISSP</h1>
<hr />
<h2><u> Commits</u></h2>
<p><br></br></p>
<h4 >Sergio</h4>
<h5><strong>r30488 | sergio | 2019-04-09 17:00:57 -0300 (Tue, 09 Apr 2019)</strong></h5>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2
<br></br></p>
<pre><code>    class cuadro_seleccion_diferida extends guarani_pers_ei_cuadro
    {
            function inicializar($parametros=array())
            {parent::inicializar($parametros);
            // Si existe el evento 'seleccion' y es de disparo diferido, se alinea a izquierda de las columnas y se genera la utilidad &quot;Todos/Ninguno&quot;.
            if ($this-&gt;existe_evento('seleccion')) {
                    $this-&gt;evento('seleccion')-&gt;set_disparo_diferido(true);
                    $this-&gt;evento('seleccion')-&gt;set_alineacion_pre_columnas(true);
                    $this-&gt;set_manejador_salida('html', 'cuadro_seleccion_diferida_salida_html');
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
            echo &quot;
            //---- Eventos ---------------------------------------------

            {$this-&gt;objeto_js}.set_evento = function(evento, hacer_submit, input)
            {
                    if (typeof hacer_submit == 'undefined') {
                            hacer_submit = true;
                    }
                    ei.prototype.set_evento.call(this, evento, hacer_submit);
            }
            &quot;;
    }
</code></pre>

<p><br></br></p>
<h4>DCelestino</h4>
<h5><strong>r31220 | dcelestino | 2019-04-15 16:48:05 -0300 (Mon, 15 Apr 2019)</strong></h5>
<ul>
<li><em>Se agregó reporte nuevo de Clases Diarias. Se modificó el reporte de Constancia de Alumno Regular. Se agregó pequeño script para posicionar el cursor en el cuadro de búsqueda al clickear sobre el menú.</em></li>
</ul>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini</p>
<pre><code>Archivo de configuración de la visualización del menú de la aplicación
menu = #
# es el número de menú, y los posibles valores de # son:
0: Menú original de Toba.
1: Menú estilo Windows.    
2: Menú estilo KDE.


menu = 1
</code></pre>

<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;jasperReport xmlns=&quot;http://jasperreports.sourceforge.net/jasperreports&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot;http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd&quot; name=&quot;guarani&quot; pageWidth=&quot;595&quot; pageHeight=&quot;842&quot; whenNoDataType=&quot;NoDataSection&quot; columnWidth=&quot;555&quot; leftMargin=&quot;20&quot; rightMargin=&quot;20&quot; topMargin=&quot;20&quot; bottomMargin=&quot;20&quot; uuid=&quot;3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8&quot;&gt;
    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.2100000000000002&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;6&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;48&quot;/&gt;
    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
    &lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
    &lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
            &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
    &lt;queryString&gt;
            &lt;![CDATA[SELECT
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
            AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
            AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
            /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
            AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
            AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
             GROUP BY
                    sga_alumnos.legajo,
                    vw_personas.apellido,
                    &lt;band splitType=&quot;Stretch&quot;/&gt;
            &lt;/columnHeader&gt;
            &lt;detail&gt;
                   &lt;band height=&quot;434&quot; splitType=&quot;Stretch&quot;&gt;
                   &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                            &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                                  &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;115&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                                  &lt;textElement textAlignment=&quot;Justified&quot;/&gt;
                                  &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                            &lt;/textField&gt;
                    &lt;line&gt;
                            &lt;reportElement x=&quot;185&quot; y=&quot;250&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                            &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;139&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;271&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;251&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                            &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField&gt;
                            &lt;reportElement x=&quot;134&quot; y=&quot;328&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                            &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;213&quot; y=&quot;199&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
                    &lt;textField&gt;
                            &lt;reportElement x=&quot;83&quot; y=&quot;363&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                            &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;staticText&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;291&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                            &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                            &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                            &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                    &lt;/staticText&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
            &lt;/band&gt;
    &lt;/detail&gt;
    &lt;columnFooter&gt;
</code></pre>

<p><br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/personalizacion.ini</p>
<pre><code>-iniciada = &quot;no&quot;
+iniciada = &quot;si&quot;
  schema_personalizado = &quot;toba_guarani_pers&quot;
  schema_original = &quot;desarrollo&quot;
</code></pre>

<p>A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co<em>clases</em>diarias.php</p>
<pre><code> class co_clases_diarias
 {

   function get_listado_vista()
   function get_listado_vista($filtro='')
    {


            /*$hoy = toba::db()-&gt;quote(guarani_fecha::get_hoy());
            $formato_fecha_hora_visual = toba::db()-&gt;quote(comunes::formato_fecha_hora_visual);*/

           if ($filtro) {
                   $where .= &quot; AND $filtro &quot;;
           }


            $sql = &quot;SELECT
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
   CONCAT(mdp_personas.apellido,' ', mdp_personas.nombres) as \&quot;docente_nombre\&quot;
          sga_propuestas.propuesta AS idpropuesta,
   array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \&quot;docente_nombre\&quot;

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
   AND mdp_personas.usuario &lt;&gt; 'Administracion'
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
                              &quot;;
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

                  if (isset($this-&gt;s__datos)) {
                   $filtro-&gt;set_datos($this-&gt;s__datos);
                  }


           }

           /**
                   */
           function evt__filtro__filtrar($datos)
           {

                  if (isset($datos)) {
                          $this-&gt;s__datos = $datos;
                          $filtro = $filtro_modalidad . $filtro_ras;
                          $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
                  } else {
                          unset($this-&gt;s__datos);
                          $this-&gt;s__filtro = '';
                  }
           }

           function conf__cuadro(toba_ei_cuadro $cuadro)
           {
                  $datos = $this-&gt;get_datos();
                  $cuadro-&gt;set_datos($datos);
                  $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());

                  /*
                  Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
                  if (isset($this-&gt;s__datos)) {
                          $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                          $cuadro-&gt;set_datos($datos);
                          $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
                  } elseif (toba::zona()-&gt;cargada()) {
                          $datos = $this-&gt;get_datos('sga_comisiones.comision = ' . toba::zona()-&gt;get_editable());
                          $cuadro-&gt;set_datos($datos);
                          $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
                  } else {
                          $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
                  }
                   $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
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
                  return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista();
                  return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista($filtro);
           }

   }


          }        
</code></pre>

<h5><strong>r31221 | dcelestino | 2019-04-15 17:43:41 -0300 (Mon, 15 Apr 2019)</strong></h5>
<ul>
<li>
<p><em>Merge de personalizaciones en testing.</em>
<br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani_clases<em>consultas</em>nuevas.php
<br></br></p>
<pre><code> static $clases = array(
       'co_clases_diarias' =&gt; array('clase'=&gt;'co_clases_diarias','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
       'co_ctrl_inasistencias' =&gt; array('clase'=&gt;'co_ctrl_inasistencia','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
       'co_inasistencias' =&gt; array('clase'=&gt;'co_inasistencias','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
       'co_inscripciones' =&gt; array('clase'=&gt;'co_inscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
       'co_inscripciones_cursadas' =&gt; array('clase'=&gt;'co_inscripciones_cursadas','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
       'co_inscriptos' =&gt; array('clase'=&gt;'co_inscriptos','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
       'co_mesas_de_examen' =&gt; array('clase'=&gt;'co_mesas_de_examen','path'=&gt;'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
       'co_preinscripciones' =&gt; array('clase'=&gt;'co_preinscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
       'co_requisitos_ingreso' =&gt; array('clase'=&gt;'co_requisitos_ingreso','path'=&gt;'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
       'co_usuarios' =&gt; array('clase'=&gt;'co_usuarios_pers','path'=&gt;'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
);
</code></pre>

</li>
</ul>
<p><br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co<em>clases</em>diarias.php
<br></br></p>
<pre><code>class co_clases_diarias
{

   function get_listado_vista($filtro='')
   {
           /*$hoy = toba::db()-&gt;quote(guarani_fecha::get_hoy());
           $formato_fecha_hora_visual = toba::db()-&gt;quote(comunes::formato_fecha_hora_visual);*/

           if ($filtro) {
                   $where .= &quot; AND $filtro &quot;;
           }


           $sql = &quot;SELECT
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
    array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \&quot;docente_nombre\&quot;

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
AND mdp_personas.usuario &lt;&gt; 'Administracion'
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
                      &quot;;
                      //die($sql);
           return guarani_db::consultar($sql);
   }

}
</code></pre>

<p><br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas
<br></br></p>
<pre><code>class ci_rep_clases_diarias extends ci_reporte
{
   protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
   protected $s__filtro_estado;
   protected $s__filtro_estado_rechazadas;

   //--------------------------------------------------------------------------
   //---- filtro --------------------------------------------------------------
   //--------------------------------------------------------------------------

   function conf__filtro(toba_ei_filtro $filtro)
   {
           if (isset($this-&gt;s__datos)) {
                   $filtro-&gt;set_datos($this-&gt;s__datos);
           }


   }

   /**
           * Redefinición del evento filtrar, para que arme una cadena WHERE acorde con la
           * nueva estructura de modalidades de cursada de comisión.
          */
   function evt__filtro__filtrar($datos)
   {
           if (isset($datos)) {
                   $this-&gt;s__datos = $datos;
                   $filtro = $filtro_modalidad . $filtro_ras;
                  $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
           } else {
                   unset($this-&gt;s__datos);
                   $this-&gt;s__filtro = '';
           }
   }

   function conf__cuadro(toba_ei_cuadro $cuadro)
   {
           if (isset($this-&gt;s__datos)) {
                   $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                  $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } elseif (toba::zona()-&gt;cargada()) {
                   $datos = $this-&gt;get_datos('sga_comisiones.comision = ' . toba::zona()-&gt;get_editable());
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } else {
                   $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
           }
           $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
   }
   function get_tabla_principal()
   {
           return 'sga_clases';
   }

   function get_datos($filtro)
   {
           return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista($filtro);
   }

   }
</code></pre>

<p><br></br></p>
<h5><strong>r31228 | dcelestino | 2019-04-16 12:02:19 -0300 (Tue, 16 Apr 2019)</strong></h5>
<ul>
<li><em>Se agregó reporte nuevo de Clases Diarias. Se modificó el reporte de Constancia de Alumno Regular. Se agregó pequeño script para posicionar el cursor en el cuadro de búsqueda al clickear sobre el menú.</em></li>
</ul>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini</p>
<pre><code>Archivo de configuración de la visualización del menú de la aplicación
menu = #
# es el número de menú, y los posibles valores de # son:
0: Menú original de Toba.
1: Menú estilo Windows.    
2: Menú estilo KDE.


menu = 1
</code></pre>

<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;jasperReport xmlns=&quot;http://jasperreports.sourceforge.net/jasperreports&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot;http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd&quot; name=&quot;guarani&quot; pageWidth=&quot;595&quot; pageHeight=&quot;842&quot; whenNoDataType=&quot;NoDataSection&quot; columnWidth=&quot;555&quot; leftMargin=&quot;20&quot; rightMargin=&quot;20&quot; topMargin=&quot;20&quot; bottomMargin=&quot;20&quot; uuid=&quot;3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8&quot;&gt;
    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.2100000000000002&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;6&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;48&quot;/&gt;
    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
    &lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
    &lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
            &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
    &lt;queryString&gt;
            &lt;![CDATA[SELECT
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
            AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
            AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
            /*AND sga_clases_asistencia_acum.comision = sga_comisiones.comision
            AND sga_clases_asistencia_acum.alumno = sga_alumnos.alumno
            AND sga_clases_asistencia_acum.tramo_quedo_libre IS NULL*/
             GROUP BY
                    sga_alumnos.legajo,
                    vw_personas.apellido,
                    &lt;band splitType=&quot;Stretch&quot;/&gt;
            &lt;/columnHeader&gt;
            &lt;detail&gt;
                   &lt;band height=&quot;434&quot; splitType=&quot;Stretch&quot;&gt;
                   &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                            &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                                  &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;115&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                                  &lt;textElement textAlignment=&quot;Justified&quot;/&gt;
                                  &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                            &lt;/textField&gt;
                    &lt;line&gt;
                            &lt;reportElement x=&quot;185&quot; y=&quot;250&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                            &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;139&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;271&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;251&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                            &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField&gt;
                            &lt;reportElement x=&quot;134&quot; y=&quot;328&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                            &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;213&quot; y=&quot;199&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
                    &lt;textField&gt;
                            &lt;reportElement x=&quot;83&quot; y=&quot;363&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                            &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;staticText&gt;
                            &lt;reportElement x=&quot;147&quot; y=&quot;291&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                            &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                            &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                            &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                    &lt;/staticText&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
            &lt;/band&gt;
    &lt;/detail&gt;
    &lt;columnFooter&gt;

          }
</code></pre>

<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas</p>
<pre><code>class ci_rep_clases_diarias extends ci_reporte
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

           if (isset($this-&gt;s__datos)) {
                   $filtro-&gt;set_datos($this-&gt;s__datos);
           }

    }

    /**

            */
    function evt__filtro__filtrar($datos)
    {

           if (isset($datos)) {
                   $this-&gt;s__datos = $datos;
                   $filtro = $filtro_modalidad . $filtro_ras;
                   $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
           } else {
                   unset($this-&gt;s__datos);
                   $this-&gt;s__filtro = '';
           }
    }

    function conf__cuadro(toba_ei_cuadro $cuadro)
    {
           $datos = $this-&gt;get_datos();
           $cuadro-&gt;set_datos($datos);
           $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());

           /*
           Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
           if (isset($this-&gt;s__datos)) {
                   $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } elseif (toba::zona()-&gt;cargada()) {
                   $datos = $this-&gt;get_datos('sga_comisiones.comision = ' . toba::zona()-&gt;get_editable());
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } else {
                   $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
           }
            $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
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
           return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista();
           return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista($filtro);
    }

}


   }
</code></pre>

<p>A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas/ci<em>rep</em>clases_diarias.php</p>
<pre><code>class ci_rep_clases_diarias extends ci_reporte
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

                  if (isset($this-&gt;s__datos)) {
                   $filtro-&gt;set_datos($this-&gt;s__datos);
                  }


           }

           /**
                   */
           function evt__filtro__filtrar($datos)
           {

                  if (isset($datos)) {
                          $this-&gt;s__datos = $datos;
                          $filtro = $filtro_modalidad . $filtro_ras;
                          $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
                  } else {
                          unset($this-&gt;s__datos);
                          $this-&gt;s__filtro = '';
                  }
           }

           function conf__cuadro(toba_ei_cuadro $cuadro)
           {
                  $datos = $this-&gt;get_datos();
                  $cuadro-&gt;set_datos($datos);
                  $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());

                  /*
                  Comento esta linea, ya que desde el Toba Editor, quité la asociacion del filtro.
                  if (isset($this-&gt;s__datos)) {
                          $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                          $cuadro-&gt;set_datos($datos);
                          $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
                  } elseif (toba::zona()-&gt;cargada()) {
                          $datos = $this-&gt;get_datos('sga_comisiones.comision = ' . toba::zona()-&gt;get_editable());
                          $cuadro-&gt;set_datos($datos);
                          $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
                  } else {
                          $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
                  }
                   $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
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
                  return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista();
                  return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista($filtro);
           }

   }


          }
</code></pre>

<p><br></br></p>
<h5><strong>r31232 | dcelestino | 2019-04-16 15:02:10 -0300 (Tue, 16 Apr 2019)</strong></h5>
<ul>
<li><em>Corrección reporte CAR.</em></li>
</ul>
<p>D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co<em>clases</em>diarias.php
class co<em>clases</em>diarias
{</p>
<pre><code>   function get_listado_vista($filtro='')
   {
           /*$hoy = toba::db()-&gt;quote(guarani_fecha::get_hoy());
           $formato_fecha_hora_visual = toba::db()-&gt;quote(comunes::formato_fecha_hora_visual);*/

           if ($filtro) {
                   $where .= &quot; AND $filtro &quot;;
           }


           $sql = &quot;SELECT
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
   /*sga_clases.tema_planificado,*/sga_clases.tema_dictado,/*sga_clases.cantidad_horas_dictadas,sga_clases_tipos.nombre AS tipo_clase_nombre,*/sga_espacios.nombre AS espacio_nombre,sga_comisiones.nombre AS nombre_comision,vw_actividades.nombre AS nombre_actividad,/*sga_comisiones.comision,*/sga_propuestas.nombre AS propuesta,sga_propuestas.propuesta AS idpropuesta,array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \&quot;docente_nombre\&quot;

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
        AND mdp_personas.usuario &lt;&gt; 'Administracion'
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
                      &quot;;
                      //die($sql);
           return guarani_db::consultar($sql);
   }

}
</code></pre>

<p><br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/cursadas</p>
<pre><code>class ci_rep_clases_diarias extends ci_reporte
{
   protected $msg_eof_cuadro = '800_eof_cuadro_sinfiltro';
   protected $s__filtro_estado;
   protected $s__filtro_estado_rechazadas;

   //--------------------------------------------------------------------------
   //---- filtro --------------------------------------------------------------
   //--------------------------------------------------------------------------

   function conf__filtro(toba_ei_filtro $filtro)
   {
           if (isset($this-&gt;s__datos)) {
                   $filtro-&gt;set_datos($this-&gt;s__datos);
           }


   }

   /**
           * Redefinición del evento filtrar, para que arme una cadena WHERE acorde con la
           * nueva estructura de modalidades de cursada de comisión.
           */
   function evt__filtro__filtrar($datos)
   {
           if (isset($datos)) {
                   $this-&gt;s__datos = $datos;
                   $filtro = $filtro_modalidad . $filtro_ras;
                   $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
           } else {
                   unset($this-&gt;s__datos);
                   $this-&gt;s__filtro = '';
           }
   }

   function conf__cuadro(toba_ei_cuadro $cuadro)
   {
           if (isset($this-&gt;s__datos)) {
                   $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } elseif (toba::zona()-&gt;cargada()) {
                   $datos = $this-&gt;get_datos('sga_comisiones.comision = ' . toba::zona()-&gt;get_editable());
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } else {
                   $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
           }
           $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
   }

   function get_tabla_principal()
   {
           return 'sga_clases';
   }

   function get_datos($filtro)
   {
           return toba::consulta_php('co_clases_diarias')-&gt;get_listado_vista($filtro);
   }

   }
</code></pre>

<p><br></br></p>
<h5><strong>r31233 | dcelestino | 2019-04-16 15:24:01 -0300 (Tue, 16 Apr 2019)</strong></h5>
<ul>
<li><em>Add personalizaciones.</em></li>
</ul>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/menu.ini
    Archivo de configuración de la visualización del menú de la aplicación</p>
<pre><code>menú = #
# es el número de menú, y los posibles valores de # son:

0: Menú original de Toba.
1: Menú estilo Windows.
2: Menú estilo KDE.
</code></pre>

<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/cursadas/co<em>clases</em>diarias.php</p>
<pre><code>   class co_clases_diarias
   {
   function get_listado_vista()
   function get_listado_vista($filtro='')
   {
            /*$hoy = toba::db()-&gt;quote(guarani_fecha::get_hoy());
            $formato_fecha_hora_visual = toba::db()-&gt;quote(comunes::formato_fecha_hora_visual);*/

    if ($filtro) {
               $where .= &quot; AND $filtro &quot;;
    }


               $sql = &quot;SELECT
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
   CONCAT(mdp_personas.apellido,' ', mdp_personas.nombres) as \&quot;docente_nombre\&quot;
          sga_propuestas.propuesta AS idpropuesta,
   array_to_string(ARRAY_AGG( mdp_personas.apellido || ' ' || mdp_personas.nombres ), ',', ' - ') AS  \&quot;docente_nombre\&quot;

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
          AND mdp_personas.usuario &lt;&gt; 'Administracion'
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
                       &quot;;
                      //die($sql);
            return guarani_db::consultar($sql);
    }
</code></pre>

<p><br></br></p>
<h5><code>r31549</code></h5>
<ul>
<li><em>Se versionan nuevamente las mismas personalizaciones: reporte de clases diarias y reporte CAR.</em></li>
</ul>
<p><br></br></p>
<h5><code>r31565</code></h5>
<ul>
<li><em>Se aplican personalizaciones anteriores.</em></li>
</ul>
<p><br></br></p>
<h5><code>r31592</code></h5>
<ul>
<li><em>Mismas personalizaciones.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r31800 | dcelestino | 2019-04-16 15:24:01 -0300 (Tue, 16 Apr 2019)</strong></h5>
<ul>
<li><em>Se agrego filtro por propuesta al reporte de mesas de examenes; también, el campo email al reporte de inscripciones a cursadas.</em></li>
</ul>
<p><br></br></p>
<pre><code>static $clases = array(
               'co_clases_diarias' =&gt; array('clase'=&gt;'co_clases_diarias','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
               'co_ctrl_inasistencias' =&gt; array('clase'=&gt;'co_ctrl_inasistencia','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
               'co_inasistencias' =&gt; array('clase'=&gt;'co_inasistencias','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
               'co_inscripciones' =&gt; array('clase'=&gt;'co_inscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
               'co_inscripciones_cursadas' =&gt; array('clase'=&gt;'co_inscripciones_cursadas','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
               'co_inscriptos' =&gt; array('clase'=&gt;'co_inscriptos','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
               'co_mesas_de_examen' =&gt; array('clase'=&gt;'co_mesas_de_examen','path'=&gt;'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
               'co_preinscripciones' =&gt; array('clase'=&gt;'co_preinscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
               'co_requisitos_ingreso' =&gt; array('clase'=&gt;'co_requisitos_ingreso','path'=&gt;'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
               'co_usuarios' =&gt; array('clase'=&gt;'co_usuarios_pers','path'=&gt;'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
        );
 }
</code></pre>

<p><br></br></p>
<h5><code>r31801</code></h5>
<ul>
<li><em>Se agrego filtro por propuesta al reporte de mesas de examenes; también, el campo email al reporte de inscripciones a cursadas.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r31839 | dcelestino | 2019-05-10 13:28:53 -0300 (Fri, 10 May 2019)</strong></h5>
<ul>
<li><em>Reporte de mesas de examenes y reporte de inscripcion a cursadas.</em></li>
</ul>
<p><br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani<em>clases</em>consultas_nuevas.php</p>
<pre><code> static $clases = array(
                'co_clases_diarias' =&gt; array('clase'=&gt;'co_clases_diarias','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
               'co_ctrl_inasistencias' =&gt; array('clase'=&gt;'co_ctrl_inasistencia','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
               'co_inasistencias' =&gt; array('clase'=&gt;'co_inasistencias','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
               'co_inscripciones' =&gt; array('clase'=&gt;'co_inscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
            'co_inscripciones_cursadas' =&gt; array('clase'=&gt;'co_inscripciones_cursadas','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
               'co_inscriptos' =&gt; array('clase'=&gt;'co_inscriptos','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
               'co_mesas_de_examen' =&gt; array('clase'=&gt;'co_mesas_de_examen','path'=&gt;'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
               'co_preinscripciones' =&gt; array('clase'=&gt;'co_preinscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
               'co_requisitos_ingreso' =&gt; array('clase'=&gt;'co_requisitos_ingreso','path'=&gt;'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
               'co_usuarios' =&gt; array('clase'=&gt;'co_usuarios_pers','path'=&gt;'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
        );
 }
</code></pre>

<p>A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/examenes/mesas<em>de</em>examen/co_mesas<em>de</em>examen.php</p>
<pre><code>            $sql = &quot;SELECT           -- Grupo 1
                                                        sga_ubicaciones.ubicacion,
                                                        sga_propuestas.propuesta,
                                                        sga_propuestas.nombre as propuesta_nombre,
                                                        sga_ubicaciones.nombre as ubicacion_nombre,
                                     -- Grupo 2
                                                        vw_actividades.elemento,
</code></pre>

<p><br></br></p>
<h5><strong>r32677 | dcelestino | 2019-06-25 10:11:19 -0300 (Tue, 25 Jun 2019)</strong></h5>
<ul>
<li><em>Personalizaciones varias de reportes.</em></li>
</ul>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/logs/conflictos.log</p>
<pre><code>Postgres dijo: ERROR:  duplicate key value violates unique constraint &quot;apex_consulta_php_pk&quot;
DETAIL:  Key (consulta_php, proyecto)=(2137000001, guarani) already exists..
El sql conflictivo es: INSERT INTO apex_consulta_php (proyecto,consulta_php,clase,archivo_clase,archivo,punto_montaje) VALUES ('guarani','2137000001','co_clases_diarias','co_clases_diarias','nucleo/cursadas/co_clases_diarias.php','34000001')
   Errores recuperables
           [W:5] El update se hizo de &lt;punto_montaje:1&gt; a &lt;punto_montaje:34000001&gt;. Ahora el valor original de la columna es &lt;punto_montaje:34000001&gt;. El registro afectado tiene clave &lt;consulta_php:41000006&gt; en la tabla &lt;apex_consulta_php&gt;
           [W:5] El update se hizo de &lt;punto_montaje:1&gt; a &lt;punto_montaje:34000001&gt;. Ahora el valor original de la columna es &lt;punto_montaje:34000001&gt;. El registro afectado tiene clave &lt;consulta_php:38000019&gt; en la tabla &lt;apex_consulta_php&gt;
Conflictos del archivo comp_2137000001.xml
    Errores fatales
            [F:2] Error de constraints en la tabla apex_objeto.
Postgres dijo: ERROR:  duplicate key value violates unique constraint &quot;apex_item_consumo_obj_pk&quot;
DETAIL:  Key (proyecto, item, objeto)=(guarani, 2137000008, 2137000006) already exists..
El sql conflictivo es: INSERT INTO apex_item_objeto (proyecto,item,objeto,orden) VALUES ('guarani','2137000008','2137000006','1')
Conflictos del archivo comp_41000059.xml
   Errores fatales
           [F:2] Error de constraints en la tabla apex_objeto_ei_cuadro_columna.
El error no fue reconocido por el importador.
Postgres dijo: ERROR:  duplicate key value violates unique constraint &quot;apex_obj_ei_cuadro_pk&quot;
DETAIL:  Key (objeto_cuadro_col, objeto_cuadro, objeto_cuadro_proyecto)=(2137000013, 41000059, guarani) already exists..
El sql conflictivo es: INSERT INTO apex_objeto_ei_cuadro_columna (objeto_cuadro_proyecto,objeto_cuadro,objeto_cuadro_col,clave,orden,titulo,estilo_titulo,estilo,ancho,formateo,no_ordenar,total,usar_vinculo,permitir_html) VALUES ('guarani','41000059','2137000013','emails','7','Email','ei-cuadro-col-tit','4','10%','1','0','0','0','0')
   Errores recuperables
           [W:5] El update se hizo de &lt;ancho:25%&gt; a &lt;ancho:20%&gt;. Ahora el valor original de la columna es &lt;ancho:20%&gt;. El registro afectado tiene clave &lt;objeto_cuadro_proyecto:guarani,objeto_cuadro:41000059,objeto_cuadro_col:41000029&gt; en la tabla &lt;apex_objeto_ei_cuadro_columna&gt;
           [W:5] El update se hizo de &lt;ancho:25%&gt; a &lt;ancho:20%&gt;. Ahora el valor original de la columna es &lt;ancho:20%&gt;. El registro afectado tiene clave &lt;objeto_cuadro_proyecto:guarani,objeto_cuadro:41000059,objeto_cuadro_col:41000032&gt; en la tabla &lt;apex_objeto_ei_cuadro_columna&gt;
Conflictos del archivo comp_41000302.xml
   Errores fatales
           [F:2] Error de constraints en la tabla apex_objeto_ei_filtro_col.
El error no fue reconocido por el importador.
Postgres dijo: ERROR:  duplicate key value violates unique constraint &quot;apex_ei_filtro_col_pk&quot;
DETAIL:  Key (objeto_ei_filtro_col, objeto_ei_filtro, objeto_ei_filtro_proyecto)=(2137000017, 41000302, guarani) already exists..
El sql conflictivo es: INSERT INTO apex_objeto_ei_filtro_col (objeto_ei_filtro_col,objeto_ei_filtro,objeto_ei_filtro_proyecto,tipo,nombre,expresion,etiqueta,obligatorio,inicial,orden,opciones_es_multiple,opciones_ef,carga_metodo,carga_consulta_php,carga_fuente,carga_col_clave,carga_col_desc,carga_permite_no_seteado,carga_no_seteado_ocultar,punto_montaje) VALUES ('2137000017','41000302','guarani','opciones','propuesta','sga_propuestas.propuesta','Propuesta','0','1','9','0','ef_combo','get_listado','5','guarani','propuesta','nombre','0','0','1')
Conflictos del archivo comp_41000119.xml
    Errores recuperables
            [W:5] El update se hizo de &lt;menu:0&gt; a &lt;menu:1&gt;. Ahora el valor original de la columna es &lt;menu:1&gt;. El registro afectado tiene clave &lt;proyecto:guarani,item:41000119&gt; en la tabla &lt;apex_item&gt;
</code></pre>

<p>M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/guarani<em>clases</em>consultas_nuevas.php</p>
<pre><code>static $clases = array(
            'co_clases_diarias' =&gt; array('clase'=&gt;'co_clases_diarias','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/co_clases_diarias.php'),
            'co_ctrl_inasistencias' =&gt; array('clase'=&gt;'co_ctrl_inasistencia','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_ctrl_inasistencia.php'),
            'co_inasistencias' =&gt; array('clase'=&gt;'co_inasistencias','path'=&gt;'../../pers_gestion/php/nucleo/asistencia/co_inasistencias.php'),
            'co_inscripciones' =&gt; array('clase'=&gt;'co_inscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscripciones.php'),
            'co_inscripciones_cursadas' =&gt; array('clase'=&gt;'co_inscripciones_cursadas','path'=&gt;'../../pers_gestion/php/nucleo/cursadas/inscripciones/co_inscripciones_cursadas.php'),
            'co_inscriptos' =&gt; array('clase'=&gt;'co_inscriptos','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/co_inscriptos.php'),
            'co_mesas_de_examen' =&gt; array('clase'=&gt;'co_mesas_de_examen','path'=&gt;'../../pers_gestion/php/nucleo/examenes/mesas_de_examen/co_mesas_de_examen.php'),
           'co_preinscripciones' =&gt; array('clase'=&gt;'co_preinscripciones','path'=&gt;'../../pers_gestion/php/nucleo/matriculas/inscripciones/propuestas_preinscripcion/co_preinscripciones.php'),
            'co_requisitos_ingreso' =&gt; array('clase'=&gt;'co_requisitos_ingreso','path'=&gt;'../../pers_gestion/php/nucleo/requisitos/requisitos_ingreso/co_requisitos_ingreso.php'),
            'co_usuarios' =&gt; array('clase'=&gt;'co_usuarios_pers','path'=&gt;'../../pers_gestion/php/nucleo/_lib/usuarios/co_usuarios_pers.php'),
    );
</code></pre>

<p>A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/operaciones/asistencia/listado_asistencias</p>
<pre><code>class ci_rep_ctrl_inasistencia extends ci_reporte
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
           return toba::consulta_php('co_inasistencias')-&gt;get_listado($filtro);
   }



   function conf__cuadro(toba_ei_cuadro $cuadro)
   {
           if (isset($this-&gt;s__datos)) {
                   $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           }  else {
                   $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
           }
           $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
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
           $filtro-&gt;columna('nombre_alumno')-&gt;set_condicion_fija('contiene');
           $filtro-&gt;columna('anio_academico')-&gt;set_condicion_fija('es_igual_a');
           $filtro-&gt;columna('periodo_lectivo')-&gt;set_condicion_fija('es_igual_a');
   }

   /**
           * Redefinici▒n del evento filtrar, para que arme una cadena WHERE acorde con la
           * nueva estructura de modalidades de cursada de comisi▒n.
           */
   function evt__filtro__filtrar($datos)
   {
           if (isset($datos)) {
                   $this-&gt;s__datos = $datos;

                   $this-&gt;s__filtro = &quot;{$this-&gt;dep('filtro')-&gt;get_sql_where()} $filtro&quot;;
           } else {
                   unset($this-&gt;s__datos);
                   $this-&gt;s__filtro = '';
           }
           /*echo '&lt;pre style=&quot;font-size:16px&quot;&gt;';
           var_dump($this-&gt;s__filtro);*/
   }

   function conf__cuadro(toba_ei_cuadro $cuadro)
   {
           if (isset($this-&gt;s__datos)) {
                   $datos = $this-&gt;get_datos($this-&gt;s__filtro);
                   $cuadro-&gt;set_datos($datos);
                   $cuadro-&gt;set_eof_mensaje($this-&gt;get_msg_eof());
           } else {
                   $cuadro-&gt;set_eof_mensaje(guarani_mensajes::get($this-&gt;msg_eof_cuadro));
           }
           $cuadro-&gt;set_filtro_asociado($this-&gt;dep('filtro'));
   }

   function get_tabla_principal()
   {
           //return 'sga_insc_cursada';
   }

   function get_datos($filtro)
   {
           /*echo '&lt;pre style=&quot;font-size:16px&quot;&gt;';
           $a = $this-&gt;dep('filtro');
           var_dump($a);
           $a-&gt;_columnas;*/
           return toba::consulta_php('co_ctrl_inasistencias')-&gt;get_listado($filtro, $this-&gt;s__datos);
   }
</code></pre>

<p><br></br></p>
<h5><code>r32688</code></h5>
<ul>
<li><em>Comandos ejecutados nuevamente.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r34459 | dcelestino | 2019-08-05 11:01:07 -0300 (Mon, 05 Aug 2019)</strong></h5>
<ul>
<li><em>Personalizaciones.</em></li>
</ul>
<p><br></br></p>
<pre><code>' as firma,
        sga_clases.clase,
        sga_asignaciones.dia_semana AS dia_semana,
        sga_clases.fecha AS fecha_clase,
        to_char(sga_clases.fecha, 'DD/MM/YYYY') AS fecha_clase,
        sga_clases.fecha,
        to_char(
                sga_asignaciones.hora_inicio,
</code></pre>

<p><br></br></p>
<h5><code>r34509</code></h5>
<ul>
<li><em>Se sube archivos co</em>clases<em>diarias.</em></li>
</ul>
<p><br></br></p>
<h5><code>r34973</code></h5>
<ul>
<li><em>Personalización de reporte de constancia de alumno regular.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r38261 | dcelestino | 2020-02-04 12:34:49 -0300 (Tue, 04 Feb 2020)</strong></h5>
<ul>
<li><em>Campos nuevos al reporte de preinscritos.</em></li>
</ul>
<p><br></br>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml</p>
<pre><code>    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
    &lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
    &lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
    &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
    &lt;parameter name=&quot;verificacion_qr&quot; class=&quot;java.lang.String&quot;/&gt;
    &lt;queryString&gt;
            &lt;![CDATA[SELECT
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
   AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
   AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
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
          LIMIT 1;]]&gt;
   &lt;/queryString&gt;
   &lt;field name=&quot;legajo&quot; class=&quot;java.lang.String&quot;&gt;
   &lt;field name=&quot;nombre_institucion&quot; class=&quot;java.lang.String&quot;&gt;
           &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
   &lt;/field&gt;
   &lt;field name=&quot;horarios&quot; class=&quot;java.lang.String&quot;/&gt;
   &lt;variable name=&quot;fecha_narrada&quot; class=&quot;java.lang.String&quot;&gt;
           &lt;variableExpression&gt;&lt;![CDATA[new java.text.SimpleDateFormat(&quot;dd 'días del mes de' MMMM 'de' yyyy&quot;, new java.util.Locale(&quot;es&quot;)).format(new java.util.Date())]]&gt;&lt;/variableExpression&gt;
   &lt;/variable&gt;
   &lt;background&gt;
           &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;&gt;
                   &lt;rectangle&gt;
                           &lt;reportElement positionType=&quot;Float&quot; x=&quot;0&quot; y=&quot;0&quot; width=&quot;555&quot; height=&quot;512&quot; uuid=&quot;02a6fe6d-f633-49df-802a-8fb70f32f883&quot;/&gt;
                           &lt;graphicElement&gt;
                                   &lt;pen lineWidth=&quot;1.5&quot;/&gt;
                           &lt;/graphicElement&gt;
                   &lt;/rectangle&gt;
           &lt;/band&gt;
           &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;/&gt;
   &lt;/background&gt;
   &lt;title&gt;
           &lt;band height=&quot;48&quot; splitType=&quot;Stretch&quot;&gt;
           &lt;band splitType=&quot;Stretch&quot;/&gt;
   &lt;/columnHeader&gt;
    &lt;detail&gt;
           &lt;band height=&quot;366&quot; splitType=&quot;Stretch&quot;&gt;
           &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                  &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;91&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                          &lt;textElement textAlignment=&quot;Justified&quot;/&gt;
                           &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot; &quot; + $F{plan_version_nombre} + &quot;, legajo Nro: &quot; +  $F{legajo} + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, &quot; + $F{provincia} + &quot; a los &quot; + $V{fecha_narrada} +&quot;.&quot;]]&gt;&lt;/textFieldExpression&gt;
                           &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                           &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                  &lt;/textField&gt;
                   &lt;staticText&gt;
                          &lt;reportElement x=&quot;131&quot; y=&quot;251&quot; width=&quot;29&quot; height=&quot;20&quot; uuid=&quot;87c75f57-6fcc-4e6f-98dc-cfae9a55c04b&quot;&gt;
                                   &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                           &lt;text&gt;&lt;![CDATA[Sello]]&gt;&lt;/text&gt;
                  &lt;/staticText&gt;
                  &lt;line&gt;
                           &lt;reportElement x=&quot;330&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                           &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                   &lt;line&gt;
                           &lt;reportElement x=&quot;83&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;e3e8256a-112d-4af9-bd3b-6c86288bd45b&quot;&gt;
                                   &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                           &lt;/reportElement&gt;
                   &lt;/line&gt;
                   &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement x=&quot;53&quot; y=&quot;114&quot; width=&quot;447&quot; height=&quot;76&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                           &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement x=&quot;264&quot; y=&quot;251&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                           &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                           &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement x=&quot;264&quot; y=&quot;271&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                           &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                           &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField&gt;
                           &lt;reportElement x=&quot;125&quot; y=&quot;298&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                           &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;image&gt;
                           &lt;reportElement x=&quot;213&quot; y=&quot;199&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                           &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
                    &lt;textField&gt;
                           &lt;reportElement x=&quot;83&quot; y=&quot;318&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                           &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                   &lt;staticText&gt;
                           &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                           &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                   &lt;/staticText&gt;
                   &lt;image&gt;
                           &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                           &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                   &lt;/image&gt;
           &lt;/band&gt;
    &lt;/detail&gt;
    &lt;columnFooter&gt;
</code></pre>

<p>A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/propuestas<em>preinscripcion/co</em>preinscripciones.php</p>
<pre><code>$datos[$key]['turno_cursada'] = $dato['turno_cursada'];
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

                            $where&quot;&quot;;

            return guarani::db()-&gt;consultar($sql);
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
                                            WHEN sga_preinscripcion_propuestas.estado = '&quot; . preinscripcion::insc_procesada . &quot;' THEN 'S▒'
                                            ELSE 'No'
                                    sga_preinscripcion
                                    JOIN sga_preinscripcion_propuestas ON
                                            sga_preinscripcion.id_preinscripcion = sga_preinscripcion_propuestas.id_preinscripcion
                                   LEFT JOIN iuse_fuerzas ON sga_preinscripcion.iuse_fuerza_descripcion = iuse_fuerzas.id
                            WHERE
                                    -- Se excluyen las Preinscripciones copiadas a G3 (se obtienen con el listado de 3w)
                                    sga_preinscripcion_propuestas.estado &lt;&gt; '&quot; . preinscripcion::insc_copiada_g3 . &quot;'
</code></pre>

<p><br></br></p>
<h5><code>r39707</code></h5>
<ul>
<li><em>Se agregó metodo para autenticar usuarios con web service.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r39912 | dcelestino | 2020-05-04 14:42:23 -0300 (Mon, 04 May 2020)</strong></h5>
<ul>
<li><em>Restricción en elección de clave.</em></li>
</ul>
<p><br></br>
D /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;jasperReport xmlns=&quot;http://jasperreports.sourceforge.net/jasperreports&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot;http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd&quot; name=&quot;guarani&quot; pageWidth=&quot;595&quot; pageHeight=&quot;842&quot; whenNoDataType=&quot;NoDataSection&quot; columnWidth=&quot;555&quot; leftMargin=&quot;20&quot; rightMargin=&quot;20&quot; topMargin=&quot;20&quot; bottomMargin=&quot;20&quot; uuid=&quot;3b7cc6f5-36a8-48bd-aa8d-b0f2b6468bf8&quot;&gt;
       &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
   &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
   &lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
   &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
   &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
   &lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
   &lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
           &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
   &lt;/parameter&gt;
   &lt;parameter name=&quot;logo&quot; class=&quot;java.lang.String&quot;/&gt;
   &lt;parameter name=&quot;autoridad_cargo&quot; class=&quot;java.lang.String&quot;&gt;
           &lt;defaultValueExpression&gt;&lt;![CDATA[&quot;&quot;]]&gt;&lt;/defaultValueExpression&gt;
   &lt;/parameter&gt;
   &lt;parameter name=&quot;autoridad_nombre&quot; class=&quot;java.lang.String&quot;&gt;
           &lt;defaultValueExpression&gt;&lt;![CDATA[&quot;Firma&quot;]]&gt;&lt;/defaultValueExpression&gt;
   &lt;/parameter&gt;
   &lt;parameter name=&quot;ocultar_firma&quot; class=&quot;java.lang.Boolean&quot;&gt;
           &lt;defaultValueExpression&gt;&lt;![CDATA[false]]&gt;&lt;/defaultValueExpression&gt;
   &lt;/parameter&gt;
   &lt;parameter name=&quot;verificacion_codigo&quot; class=&quot;java.lang.String&quot;/&gt;
   &lt;parameter name=&quot;verificacion_url&quot; class=&quot;java.lang.String&quot;/&gt;
   &lt;parameter name=&quot;verificacion_qr&quot; class=&quot;java.lang.String&quot;/&gt;
   &lt;queryString&gt;
           &lt;![CDATA[SELECT
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
 AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
 AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
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
 LIMIT 1;]]&gt;
       &lt;/queryString&gt;
       &lt;field name=&quot;legajo&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;apellido_y_nombre&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;documento_principal&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;propuesta_nombre&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;propuesta_nombre_completo&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;propuesta_nombre_abreviado&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;ubicacion_nombre&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;plan_nombre&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;plan_version_nombre&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;presentar_a&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;observaciones&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;ciudad&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;provincia&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;nombre_institucion&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
       &lt;/field&gt;
       &lt;field name=&quot;horarios&quot; class=&quot;java.lang.String&quot;/&gt;
       &lt;variable name=&quot;fecha_narrada&quot; class=&quot;java.lang.String&quot;&gt;
               &lt;variableExpression&gt;&lt;![CDATA[new java.text.SimpleDateFormat(&quot;dd 'días del mes de' MMMM 'de' yyyy&quot;, new java.util.Locale(&quot;es&quot;)).format(new java.util.Date())]]&gt;&lt;/variableExpression&gt;
       &lt;/variable&gt;
       &lt;background&gt;
               &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;/&gt;
       &lt;/background&gt;
       &lt;title&gt;
               &lt;band height=&quot;48&quot; splitType=&quot;Stretch&quot;&gt;
                       &lt;staticText&gt;
                               &lt;reportElement style=&quot;Title&quot; x=&quot;185&quot; y=&quot;12&quot; width=&quot;328&quot; height=&quot;23&quot; uuid=&quot;ee936c70-4673-4302-b64f-af7d7fead711&quot;/&gt;
                               &lt;text&gt;&lt;![CDATA[Constancia de Alumno Regular]]&gt;&lt;/text&gt;
                       &lt;/staticText&gt;
                       &lt;image&gt;
                               &lt;reportElement x=&quot;42&quot; y=&quot;5&quot; width=&quot;92&quot; height=&quot;40&quot; uuid=&quot;9749d392-5fc0-48de-98e6-37ab50f757a3&quot;/&gt;
                               &lt;imageExpression&gt;&lt;![CDATA[$P{logo}]]&gt;&lt;/imageExpression&gt;
                       &lt;/image&gt;
               &lt;/band&gt;
       &lt;/title&gt;
       &lt;pageHeader&gt;
               &lt;band splitType=&quot;Stretch&quot;/&gt;
       &lt;/pageHeader&gt;
       &lt;columnHeader&gt;
               &lt;band splitType=&quot;Stretch&quot;/&gt;
       &lt;/columnHeader&gt;
       &lt;detail&gt;
               &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                       &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                               &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                               &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;line&gt;
                               &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                       &lt;/line&gt;
                       &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                               &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                       &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                               &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                               &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                               &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                               &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;textField&gt;
                               &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                               &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;image&gt;
                               &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                               &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                       &lt;/image&gt;
                       &lt;textField&gt;
                               &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                       &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                               &lt;/reportElement&gt;
                               &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                       &lt;/textField&gt;
                       &lt;staticText&gt;
                               &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                               &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                       &lt;/staticText&gt;
                       &lt;image&gt;
                               &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                               &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                      &lt;/image&gt;
               &lt;/band&gt;
       &lt;/detail&gt;
       &lt;columnFooter&gt;
           &lt;band splitType=&quot;Stretch&quot;/&gt;
       &lt;/columnFooter&gt; 
       &lt;pageFooter&gt;
           &lt;band splitType=&quot;Stretch&quot;/&gt;
       &lt;/pageFooter&gt;
       &lt;summary&gt;
           &lt;band splitType=&quot;Stretch&quot;/&gt;
       &lt;/summary&gt;
&lt;/jasperReport&gt;
</code></pre>

<p>M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/<em>lib/usuarios/usuario.php
class usuario extends usuario</em>nucleo {</p>
<pre><code>static function validar_clave_permitida($clave)
{
           // Se controla la longitud mínima de la contraseña.
           // Se realiza el pedido anulando el uso de caché, debido a que este parámetro a nivel Institución
           // es consumido también desde Autogestión
           $longitud_minima = guarani::parametros()-&gt;get_valor('login_clave_longitud_minima', null, false);
           //permitimos solo letras y/o numeros en la clave
           $patron_valido =  (preg_match (&quot;/^[a-zA-Z0-9]+$/&quot;, $clave)) ? true : false;
           return ((strlen($clave) &gt;= $longitud_minima) &amp;&amp; $patron_valido);
   }
 }
</code></pre>

<p><br></br></p>
<h5><code>r48082</code></h5>
<ul>
<li><em>Filtros &quot;pertenece a fuerzas de seguridad&quot;  en reporte de preinscritos.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r48509 | dcelestino | 2021-03-12 12:56:33 -0300 (Fri, 12 Mar 2021)</strong></h5>
<ul>
<li><em>Se agregó campo mail al reporte de inscripción a propuestas.</em></li>
</ul>
<p><br></br>
M/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/co_inscripciones.php</p>
<pre><code>*/
        function get_inscriptos_perfil_de_datos($where = '')
        {

               /*$condiciones = explode('AND', $where);
               $condicion = explode('=', $condiciones[0]);
               $anio = $condicion[1];*/
               $sql = &quot;SELECT  nro_documento,
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
                               LEFT JOIN iuse_fuerzas ON iuse_fuerzas.id = sga_preinscripcion.iuse_fuerza_descripcion&quot;;
               $datos_preinscripcion = toba::db('preinscripcion')-&gt;consultar($sql);
               //echo '&lt;h1&gt;&lt;br /&gt;&lt;br /&gt;';
               //var_dump($datos_preinscripcion[0][0]);
               //die();
               // $key = array_search('31210111', array_column($datos_preinscripcion, 'nro_documento'));


                if ($where) {
                        $where = &quot;WHERE $where&quot;;
                }
                $sql = &quot;SELECT

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
                &quot;;
               return guarani_db::consultar($sql);

               $datos_gestion = guarani_db::consultar($sql);
               /*
               iuse_pertenece_fuerzas_seguridad,
                                              iuse_fuerza_descripcion,
                                               iuse_otras_policias_provinciales,
                                               iuse_grado_en_fuerza,
                                               iuse_antiguedad_general_fuerza
               */
               foreach($datos_gestion as $k =&gt; $v){
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
</code></pre>

<p><br></br></p>
<h5><strong>r48703 | dcelestino | 2021-03-25 14:12:28 -0300 (Thu, 25 Mar 2021)</strong></h5>
<ul>
<li><em>Se agregaron campos al reporte de inscripcion a propuestas. &quot;pertenece o no&quot; a fuerzas policiales.</em></li>
</ul>
<p><br></br>
M/nodos/iuse/gestion/trunk/3.16.2/personalizacion/php/nucleo/matriculas/inscripciones/co_inscripciones.php</p>
<pre><code>WHEN sga_preinscripcion.iuse_pertenece_fuerzas_seguridad = 0 THEN 'No'
                                                ELSE ''
                                        END as pertenece_fuerzas,
                                        sga_preinscripcion.iuse_grado_en_fuerza,
                                        iuse_fuerzas.nombre as fuerza_nombre,
                                        iuse_otras_policias_provinciales,
                                        iuse_grado_en_fuerza,
</code></pre>

<p><br></br></p>
<h5><code>r53949</code></h5>
<ul>
<li><em>Se agregó una coma luego del apellido del alumno.</em></li>
</ul>
<p><br></br></p>
<h5><code>r54795</code></h5>
<ul>
<li><em>Se agrega campo nuevo al reporte de inscriptos por propuestas.</em></li>
</ul>
<p><br></br></p>
<h5><strong>r55537 | dcelestino | 2021-10-18 11:24:10 -0300 (Mon, 18 Oct 2021)</strong></h5>
<ul>
<li><em>Se corrige constancia alumno regular, se cortaba el texto que indica los horarios del alumno.</em></li>
</ul>
<p><br></br>
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaRegular.jrxml</p>
<pre><code>&lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
    &lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
    &lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
    &lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
            &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
    &lt;parameter name=&quot;verificacion_qr&quot; class=&quot;java.lang.String&quot;/&gt;
    &lt;queryString&gt;
            &lt;![CDATA[SELECT
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
    AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
    AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
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
     LIMIT 1;]]&gt;
            &lt;/queryString&gt;
            &lt;field name=&quot;legajo&quot; class=&quot;java.lang.String&quot;&gt;

            &lt;field name=&quot;nombre_institucion&quot; class=&quot;java.lang.String&quot;&gt;
            &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
            &lt;/field&gt;
            &lt;field name=&quot;horarios&quot; class=&quot;java.lang.String&quot;/&gt;
            &lt;variable name=&quot;fecha_narrada&quot; class=&quot;java.lang.String&quot;&gt;
            &lt;variableExpression&gt;&lt;![CDATA[new java.text.SimpleDateFormat(&quot;dd 'días del mes de' MMMM 'de' yyyy&quot;, new java.util.Locale(&quot;es&quot;)).format(new java.util.Date())]]&gt;&lt;/variableExpression&gt;
            &lt;/variable&gt;
    &lt;background&gt;
           &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;&gt;
                    &lt;rectangle&gt;
                            &lt;reportElement positionType=&quot;Float&quot; x=&quot;0&quot; y=&quot;0&quot; width=&quot;555&quot; height=&quot;512&quot; uuid=&quot;02a6fe6d-f633-49df-802a-8fb70f32f883&quot;/&gt;
                            &lt;graphicElement&gt;
                                   &lt;pen lineWidth=&quot;1.5&quot;/&gt;
                            &lt;/graphicElement&gt;
                    &lt;/rectangle&gt;
            &lt;/band&gt;
                   &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;/&gt;
    &lt;/background&gt;
    &lt;title&gt;
            &lt;band height=&quot;48&quot; splitType=&quot;Stretch&quot;&gt;
            &lt;band splitType=&quot;Stretch&quot;/&gt;
    &lt;/columnHeader&gt;
    &lt;detail&gt;
            &lt;band height=&quot;366&quot; splitType=&quot;Stretch&quot;&gt;
                   &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;91&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                            &lt;textElement textAlignment=&quot;Justified&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot; &quot; + $F{plan_version_nombre} + &quot;, legajo Nro: &quot; +  $F{legajo} + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, &quot; + $F{provincia} + &quot; a los &quot; + $V{fecha_narrada} +&quot;.&quot;]]&gt;&lt;/textFieldExpression&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                           &lt;staticText&gt;
                                   &lt;reportElement x=&quot;131&quot; y=&quot;251&quot; width=&quot;29&quot; height=&quot;20&quot; uuid=&quot;87c75f57-6fcc-4e6f-98dc-cfae9a55c04b&quot;&gt;
                                           &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                                   &lt;/reportElement&gt;
                                   &lt;text&gt;&lt;![CDATA[Sello]]&gt;&lt;/text&gt;
                           &lt;/staticText&gt;
                    &lt;line&gt;
                                   &lt;reportElement x=&quot;330&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                           &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                           &lt;line&gt;
                            &lt;reportElement x=&quot;83&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;e3e8256a-112d-4af9-bd3b-6c86288bd45b&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;114&quot; width=&quot;447&quot; height=&quot;76&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;264&quot; y=&quot;251&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                            &lt;reportElement x=&quot;264&quot; y=&quot;271&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                            &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField&gt;
                           &lt;reportElement x=&quot;125&quot; y=&quot;298&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                           &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;213&quot; y=&quot;199&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                            &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
                    &lt;textField&gt;
                            &lt;reportElement x=&quot;83&quot; y=&quot;318&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                            &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;staticText&gt;
                            &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                            &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                    &lt;/staticText&gt;
                    &lt;image&gt;
                            &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                    &lt;/image&gt;
            &lt;/band&gt;
    &lt;/detail&gt;
    &lt;columnFooter&gt;
</code></pre>

<p><br></br></p>
<h5><strong>r57038 | dcelestino | 2021-11-26 11:18:20 -0300 (Fri, 26 Nov 2021)</strong></h5>
<ul>
<li><em>Modificación de reporte de constancia de actividades aprobadas.</em></li>
</ul>
<p><br></br>
A/nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaActividadesAprobadas.jrxml</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;!-- Created with Jaspersoft Studio version 6.18.1.final using JasperReports Library version 6.18.1-9d75d1969e774d4f179fb3be8401e98a0e6d1611  --&gt;
&lt;jasperReport xmlns=&quot;http://jasperreports.sourceforge.net/jasperreports&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot;http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd&quot; name=&quot;guarani&quot; language=&quot;groovy&quot; pageWidth=&quot;595&quot; pageHeight=&quot;842&quot; columnWidth=&quot;555&quot; leftMargin=&quot;20&quot; rightMargin=&quot;20&quot; topMargin=&quot;20&quot; bottomMargin=&quot;20&quot; uuid=&quot;d025d606-8fcc-4325-a190-2fdb26fba675&quot;&gt;
    &lt;property name=&quot;ireport.zoom&quot; value=&quot;1.4641000000000006&quot;/&gt;
    &lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
                                            &lt;connectionExpression&gt;&lt;![CDATA[$P{REPORT_CONNECTION}]]&gt;&lt;/connectionExpression&gt;
                                    &lt;/datasetRun&gt;
                                    &lt;jr:listContents height=&quot;19&quot;&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; stretchType=&quot;RelativeToTallestObject&quot; x=&quot;19&quot; y=&quot;0&quot; width=&quot;160&quot; height=&quot;18&quot; uuid=&quot;d3842c1a-cdc9-440b-834e-8e983187215f&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{actividad_descr}]]&gt;&lt;/textFieldExpression&gt;
                                            &lt;/textField&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; x=&quot;179&quot; y=&quot;1&quot; width=&quot;69&quot; height=&quot;17&quot; uuid=&quot;8ae02570-e798-4bf0-bfe1-628920db5f81&quot;/&gt;
                                                    &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{fecha}]]&gt;&lt;/textFieldExpression&gt;
                                            &lt;/textField&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; x=&quot;248&quot; y=&quot;1&quot; width=&quot;69&quot; height=&quot;17&quot; uuid=&quot;b917354c-1a12-4b2f-9861-716d6af8bdca&quot;/&gt;
                                                    &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{nota_completa}]]&gt;&lt;/textFieldExpression&gt;
                                            &lt;/textField&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; stretchType=&quot;RelativeToTallestObject&quot; x=&quot;317&quot; y=&quot;1&quot; width=&quot;97&quot; height=&quot;17&quot; uuid=&quot;c07e2087-5858-4fd6-b10a-96dd26a11cef&quot;/&gt;
                                                    &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{tipo}]]&gt;&lt;/textFieldExpression&gt;
                                            &lt;/textField&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; stretchType=&quot;RelativeToTallestObject&quot; x=&quot;415&quot; y=&quot;1&quot; width=&quot;69&quot; height=&quot;17&quot; uuid=&quot;d1b69011-8b89-4193-8a8d-4bca5d64de03&quot;/&gt;
                                                    &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{actividad_documento}]]&gt;&lt;/textFieldExpression&gt;
                                            &lt;/textField&gt;
                                           &lt;textField isStretchWithOverflow=&quot;true&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                           &lt;textField textAdjust=&quot;StretchHeight&quot; isBlankWhenNull=&quot;true&quot;&gt;
                                                    &lt;reportElement style=&quot;Comun&quot; x=&quot;483&quot; y=&quot;1&quot; width=&quot;52&quot; height=&quot;17&quot; uuid=&quot;3d053b94-ee57-46d4-8db4-ba0db7ca9198&quot;/&gt;
                                                    &lt;textElement textAlignment=&quot;Center&quot;/&gt;
                                                    &lt;textFieldExpression&gt;&lt;![CDATA[$F{folio_fisico}]]&gt;&lt;/textFieldExpression&gt;
    &lt;summary&gt;
            &lt;band height=&quot;314&quot; splitType=&quot;Stretch&quot;&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement style=&quot;Comun&quot; x=&quot;287&quot; y=&quot;185&quot; width=&quot;206&quot; height=&quot;20&quot; uuid=&quot;1a4d4b61-9022-4648-8cc1-8c72e5672e55&quot;&gt;
                           &lt;reportElement style=&quot;Comun&quot; x=&quot;190&quot; y=&quot;182&quot; width=&quot;206&quot; height=&quot;20&quot; uuid=&quot;1a4d4b61-9022-4648-8cc1-8c72e5672e55&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Top&quot;&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                           &lt;reportElement style=&quot;Comun&quot; x=&quot;287&quot; y=&quot;205&quot; width=&quot;206&quot; height=&quot;20&quot; uuid=&quot;a94115c7-72d5-45a9-9758-31a1ba8fdfa3&quot;&gt;
                           &lt;reportElement style=&quot;Comun&quot; x=&quot;190&quot; y=&quot;202&quot; width=&quot;206&quot; height=&quot;20&quot; uuid=&quot;a94115c7-72d5-45a9-9758-31a1ba8fdfa3&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Top&quot;&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;line&gt;
                           &lt;reportElement x=&quot;325&quot; y=&quot;183&quot; width=&quot;130&quot; height=&quot;1&quot; forecolor=&quot;#000000&quot; uuid=&quot;8d93bf9d-4873-4ab3-bc3d-cdc8def1ab07&quot;&gt;
                           &lt;reportElement x=&quot;217&quot; y=&quot;180&quot; width=&quot;130&quot; height=&quot;1&quot; forecolor=&quot;#000000&quot; uuid=&quot;8d93bf9d-4873-4ab3-bc3d-cdc8def1ab07&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                    &lt;/line&gt;
                   &lt;staticText&gt;
                           &lt;reportElement style=&quot;Resalt&quot; x=&quot;105&quot; y=&quot;185&quot; width=&quot;29&quot; height=&quot;20&quot; uuid=&quot;6927d449-1c9f-453a-9767-fac06693f137&quot;&gt;
                                   &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                           &lt;/reportElement&gt;
                           &lt;textElement textAlignment=&quot;Center&quot;&gt;
                                   &lt;font isBold=&quot;false&quot; pdfFontName=&quot;Helvetica&quot;/&gt;
                           &lt;/textElement&gt;
                           &lt;text&gt;&lt;![CDATA[Sello]]&gt;&lt;/text&gt;
                   &lt;/staticText&gt;
                   &lt;line&gt;
                           &lt;reportElement x=&quot;54&quot; y=&quot;184&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;6d471a23-4fe1-4a9d-a764-020ae862d947&quot;&gt;
                                   &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                           &lt;/reportElement&gt;
                   &lt;/line&gt;
                    &lt;textField&gt;
                            &lt;reportElement style=&quot;Comun&quot; x=&quot;48&quot; y=&quot;64&quot; width=&quot;447&quot; height=&quot;41&quot; uuid=&quot;86bc625f-82b7-4b7c-8c63-18cc52d350be&quot;/&gt;
                            &lt;textElement textAlignment=&quot;Justified&quot;&gt;
                            &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                    &lt;/textField&gt;
                    &lt;image&gt;
                           &lt;reportElement x=&quot;222&quot; y=&quot;113&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;d251c01a-f333-4709-b450-9c7314283418&quot;&gt;
                           &lt;reportElement x=&quot;42&quot; y=&quot;110&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;d251c01a-f333-4709-b450-9c7314283418&quot;&gt;
                                    &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                            &lt;/reportElement&gt;
                            &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
</code></pre>

<p><br></br></p>
<h5><strong>r59597 | dcelestino | 2022-04-11 11:04:37 -0300 (Mon, 11 Apr 2022)</strong></h5>
<ul>
<li>
<p><em>se agrega firma de nessi añl reporte de constancia de materias aprobadas.</em>
M /nodos/iuse/gestion/trunk/3.16.2/personalizacion/exportaciones/jasper/ConstanciaActividadesAprobadas.jrxml
A /nodos/iuse/gestion/trunk/3.16.2/personalizacion/www/img/firma<em>nessi</em>small.png</p>
<pre><code>&lt;property name=&quot;ireport.zoom&quot; value=&quot;1.0&quot;/&gt;
&lt;property name=&quot;ireport.x&quot; value=&quot;0&quot;/&gt;
&lt;property name=&quot;ireport.y&quot; value=&quot;0&quot;/&gt;
&lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w1&quot; value=&quot;430&quot;/&gt;
&lt;property name=&quot;com.jaspersoft.studio.data.sql.SQLQueryDesigner.sash.w2&quot; value=&quot;564&quot;/&gt;
&lt;style name=&quot;Title&quot; fontName=&quot;Times New Roman&quot; fontSize=&quot;14&quot; isBold=&quot;true&quot; isUnderline=&quot;true&quot; pdfFontName=&quot;Times-Bold&quot;/&gt;
&lt;parameter name=&quot;solicitud&quot; class=&quot;java.lang.Integer&quot;&gt;
        &lt;defaultValueExpression&gt;&lt;![CDATA[new Integer(1)]]&gt;&lt;/defaultValueExpression&gt;
&lt;parameter name=&quot;verificacion_qr&quot; class=&quot;java.lang.String&quot;/&gt;
&lt;queryString&gt;
        &lt;![CDATA[SELECT
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
 AND sga_periodos_lectivos.fecha_inicio_dictado &lt; NOW()::DATE
 AND sga_periodos_lectivos.fecha_fin_dictado &gt; NOW()::DATE
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
LIMIT 1;]]&gt;
 &lt;/queryString&gt;
 &lt;field name=&quot;legajo&quot; class=&quot;java.lang.String&quot;&gt;
 &lt;field name=&quot;nombre_institucion&quot; class=&quot;java.lang.String&quot;&gt;
         &lt;fieldDescription&gt;&lt;![CDATA[]]&gt;&lt;/fieldDescription&gt;
 &lt;/field&gt;
 &lt;field name=&quot;horarios&quot; class=&quot;java.lang.String&quot;/&gt;
 &lt;variable name=&quot;fecha_narrada&quot; class=&quot;java.lang.String&quot;&gt;
         &lt;variableExpression&gt;&lt;![CDATA[new java.text.SimpleDateFormat(&quot;dd 'días del mes de' MMMM 'de' yyyy&quot;, new java.util.Locale(&quot;es&quot;)).format(new java.util.Date())]]&gt;&lt;/variableExpression&gt;
 &lt;/variable&gt;
 &lt;background&gt;
         &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;&gt;
                 &lt;rectangle&gt;
                         &lt;reportElement positionType=&quot;Float&quot; x=&quot;0&quot; y=&quot;0&quot; width=&quot;555&quot; height=&quot;512&quot; uuid=&quot;02a6fe6d-f633-49df-802a-8fb70f32f883&quot;/&gt;
                         &lt;graphicElement&gt;
                                 &lt;pen lineWidth=&quot;1.5&quot;/&gt;
                         &lt;/graphicElement&gt;
                 &lt;/rectangle&gt;
         &lt;/band&gt;
         &lt;band height=&quot;546&quot; splitType=&quot;Stretch&quot;/&gt;
 &lt;/background&gt;
 &lt;title&gt;
         &lt;band height=&quot;48&quot; splitType=&quot;Stretch&quot;&gt;
         &lt;band splitType=&quot;Stretch&quot;/&gt;
 &lt;/columnHeader&gt;
 &lt;detail&gt;
         &lt;band height=&quot;366&quot; splitType=&quot;Stretch&quot;&gt;
         &lt;band height=&quot;653&quot; splitType=&quot;Stretch&quot;&gt;
                  &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                         &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;91&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                         &lt;textElement textAlignment=&quot;Justified&quot;/&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot; &quot; + $F{plan_version_nombre} + &quot;, legajo Nro: &quot; +  $F{legajo} + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, &quot; + $F{provincia} + &quot; a los &quot; + $V{fecha_narrada} +&quot;.&quot;]]&gt;&lt;/textFieldExpression&gt;
                         &lt;reportElement x=&quot;53&quot; y=&quot;13&quot; width=&quot;447&quot; height=&quot;209&quot; uuid=&quot;e716409d-f2dd-4889-a9b1-d6b9f1d7d764&quot;/&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[&quot;La sección alumnado de el/la &quot; + $F{nombre_institucion} + &quot; certifica que &quot; + $F{apellido_y_nombre}.toUpperCase() + &quot; con &quot; + $F{documento_principal} + &quot; está inscripto(/a) como alumno(/a) regular en la propuesta de &quot; + $F{propuesta_nombre}.toUpperCase() + &quot;. A su pedido y para su presentación ante &quot; + $F{presentar_a}.toUpperCase() + &quot; se le extiende la presente en &quot; + $F{ciudad} + &quot;, a los &quot; + $V{fecha_narrada} +&quot;. \nHorarios: &quot; + $F{horarios}]]&gt;&lt;/textFieldExpression&gt;
                  &lt;/textField&gt;
                  &lt;staticText&gt;
                         &lt;reportElement x=&quot;131&quot; y=&quot;251&quot; width=&quot;29&quot; height=&quot;20&quot; uuid=&quot;87c75f57-6fcc-4e6f-98dc-cfae9a55c04b&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;text&gt;&lt;![CDATA[Sello]]&gt;&lt;/text&gt;
                 &lt;/staticText&gt;
                 &lt;line&gt;
                         &lt;reportElement x=&quot;330&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                         &lt;reportElement x=&quot;185&quot; y=&quot;420&quot; width=&quot;182&quot; height=&quot;1&quot; uuid=&quot;f8b38d59-8c6e-464a-be45-68347b7297a0&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                 &lt;/line&gt;
                 &lt;line&gt;
                         &lt;reportElement x=&quot;83&quot; y=&quot;250&quot; width=&quot;130&quot; height=&quot;1&quot; uuid=&quot;e3e8256a-112d-4af9-bd3b-6c86288bd45b&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                 &lt;/line&gt;
                 &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                         &lt;reportElement x=&quot;53&quot; y=&quot;114&quot; width=&quot;447&quot; height=&quot;76&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                         &lt;reportElement x=&quot;53&quot; y=&quot;239&quot; width=&quot;447&quot; height=&quot;60&quot; uuid=&quot;e418a161-258f-44f3-b39d-fe2ecdbd0057&quot;/&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[((($F{observaciones}.trim()).isEmpty()) ? &quot;&quot; : (&quot;OBSERVACIONES: &quot; + $F{observaciones}))]]&gt;&lt;/textFieldExpression&gt;
                 &lt;/textField&gt;
                 &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                         &lt;reportElement x=&quot;264&quot; y=&quot;251&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                         &lt;reportElement x=&quot;230&quot; y=&quot;450&quot; width=&quot;220&quot; height=&quot;20&quot; uuid=&quot;b5811651-8d92-48a8-b842-ec2224484307&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_nombre}]]&gt;&lt;/textFieldExpression&gt;
                 &lt;/textField&gt;
                 &lt;textField isBlankWhenNull=&quot;true&quot;&gt;
                         &lt;reportElement x=&quot;264&quot; y=&quot;271&quot; width=&quot;261&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                         &lt;reportElement x=&quot;220&quot; y=&quot;432&quot; width=&quot;258&quot; height=&quot;20&quot; uuid=&quot;a4589143-fb55-4d0b-9d67-591e08735960&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[($P{ocultar_firma}.booleanValue() == false)]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;textElement textAlignment=&quot;Center&quot; verticalAlignment=&quot;Middle&quot;/&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[$P{autoridad_cargo}]]&gt;&lt;/textFieldExpression&gt;
                 &lt;/textField&gt;
                 &lt;textField&gt;
                         &lt;reportElement x=&quot;125&quot; y=&quot;298&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                         &lt;reportElement x=&quot;127&quot; y=&quot;510&quot; width=&quot;300&quot; height=&quot;20&quot; uuid=&quot;200650ae-706e-401d-acf0-2534b488e940&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[&quot;CÓDIGO DE VALIDACIÓN: &quot; + $P{verificacion_codigo}]]&gt;&lt;/textFieldExpression&gt;
                 &lt;/textField&gt;
                 &lt;image&gt;
                         &lt;reportElement x=&quot;213&quot; y=&quot;199&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                         &lt;reportElement x=&quot;230&quot; y=&quot;289&quot; width=&quot;92&quot; height=&quot;92&quot; uuid=&quot;62120307-e032-45a9-a72a-05e9469a2986&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;imageExpression&gt;&lt;![CDATA[$P{verificacion_qr}]]&gt;&lt;/imageExpression&gt;
                 &lt;/image&gt;
                 &lt;textField&gt;
                         &lt;reportElement x=&quot;83&quot; y=&quot;318&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                         &lt;reportElement x=&quot;76&quot; y=&quot;560&quot; width=&quot;417&quot; height=&quot;48&quot; uuid=&quot;5d811c69-acde-41c8-8f89-04c6cf482e6a&quot;&gt;
                                 &lt;printWhenExpression&gt;&lt;![CDATA[!($P{verificacion_qr}.trim()).isEmpty()]]&gt;&lt;/printWhenExpression&gt;
                         &lt;/reportElement&gt;
                         &lt;textFieldExpression&gt;&lt;![CDATA[&quot;Este certificado podrá ser validado ingresando a &quot; + $P{verificacion_url}+ &quot; completando el código de validación y el Nº de DNI (o pasaporte) del alumno o bien escaneando el código QR.&quot;]]&gt;&lt;/textFieldExpression&gt;
                 &lt;/textField&gt;
                 &lt;staticText&gt;
                         &lt;reportElement x=&quot;250&quot; y=&quot;470&quot; width=&quot;128&quot; height=&quot;20&quot; uuid=&quot;53d8d55d-d87a-46da-a013-345ba8b7ee91&quot;/&gt;
                         &lt;text&gt;&lt;![CDATA[IUSE]]&gt;&lt;/text&gt;
                 &lt;/staticText&gt;
                 &lt;image&gt;
                         &lt;reportElement x=&quot;222&quot; y=&quot;313&quot; width=&quot;100&quot; height=&quot;97&quot; uuid=&quot;590eee88-216f-427a-a99f-2d8504ffa57a&quot;/&gt;
                         &lt;imageExpression&gt;&lt;![CDATA[&quot;/home/insusep/guarani/personalizacion/www/img/firma_nessi_small.png&quot;]]&gt;&lt;/imageExpression&gt;
                 &lt;/image&gt;
         &lt;/band&gt;
 &lt;/detail&gt;
 &lt;columnFooter&gt;
 Index: www/img/firma_nessi_small.png
</code></pre>

</li>
</ul>
<p><br></br></p>
<h5><strong>r59622 | dcelestino | 2022-04-12 10:37:20 -0300 (Tue, 12 Apr 2022)</strong></h5>
<ul>
<li><em>Se corrige firma en constancia de actividades aprobadas, y se agrega firma a reporte de constancia de alumno regular.</em></li>
</ul>
<p><br></br></p>
<hr />
<h2>Imágenes correspondientes al historial de actualizaciones</h2>
<p><br></br></p>
<h4>Desarrollo de reporte nuevo de Clases Diarias</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1AlduaVhEuKBrGmrOaIerd8rWo3A6dShf" alt="Screenshot que muestra el reporte de clases diarias." title="Desarrollo de reporte nuevo de Clases Diarias" /></p>
<h4>Se modificó el reporte de Constancia de Alumno Regular</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1phzdNN2Wp6mBYRhas1xidxJ5KJ5EcX2m" alt="Screenshot constancia de alumno regular." title="Se modificó el reporte de Constancia de Alumno Regular " /></p>
<h4>Se desarrolló script para posicionar el cursor en el cuadro de búsqueda al clickear en el menú</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1hHtHv1qrEtN3614VVw9txmvyJwh4Kvxx" alt="Screenshot mostrando el posicionamiento del cursor" title="Se desarrolló script para posicionar el cursor en el cuadro de búsqueda al clickear en el menú" /></p>
<h4>Se agrego filtro por propuesta al reporte de mesas de exámenes</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1VQXlpP5j0hKcuG52Z2kznXOqMNKHOKAM" alt="Screenshot mostrando el filtro agregado." title="Se agrego filtro por propuesta al reporte de mesas de exámenes" /></p>
<h4>Se agrego el campo email al reporte de inscripciones a cursadas</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1ULJSGQAuU2mEkK8Zk-cvy2-Fr5uiDNfP" alt="Screenshot señalando el campo agregado." title="Se agrego el campo email al reporte de inscripciones a cursadas" /></p>
<h4>Campos nuevos al reporte de preinscriptos</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1BvDxeTPx_ToHQD-ZyLnydDMgE0Z0d7np" alt="Screenshot recuadrando este reporte nuevo." title="Desarrollo de reporte nuevo de Clases Diarias" /></p>
<h4>Se desarrolló webservice para autenticarse</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1KIFPzPXpvUoqTWwycJEKgzYsTinvoeNG" alt="Servicio de webservice para autenticación." title="Se desarrolló webservice para autenticarse " /></p>
<h4>Restricción en elección de clave al generar contraseña</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1Dloz4WiLlFEhB_6rzJtpIr7qBVkPrkWU" alt="Screenshot mostrando los requisitos para llevar a cabo la generacón de contraseña" title="Restricción en elección de clave al generar contraseña" /></p>
<h4>Filtros &quot;pertenece a fuerzas de seguridad&quot; en reporte de preinscritos</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1vFJf-jUO24NgvzfAXwUf7zwIulP17OGR" alt="Screenshot señalando el filtro que denota lo indicado." title="Filtros &quot;pertenece a fuerzas de seguridad&quot; en reporte de preinscritos " /></p>
<h4>Se agregó campo mail al reporte de inscripción a propuestas</h4>
<p><img src="http://drive.google.com/uc?export=view&amp;id=1-fqkbmZOcalfFTs8jCEXUQrpcdd8f7oq" alt="Muestra del agregado del campo mail." title="Se agregó campo mail al reporte de inscripción a propuestas" /></p>

</div>
   


</body>
</html> 
