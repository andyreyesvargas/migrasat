<h1>Gestión de Políticas de Seguridad Openscap</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la Gestión de Políticas de Seguridad Openscap.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Politica de seguridad de OpenSCAP completa con Satellite. (Demostrativo)
 <br>- Politica de seguridad de OpenSCAP customizada con Satellite. (Demostrativo)
 <br>- Remediación de politica de seguridad de OpenSCAP con Satellite. (Demostrativo)
</p>
<p>
<strong>Secciones:</strong>
<br>- Habilitación de Red Hat Insights en servidor Satellite. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>
</p>

## Politica de seguridad de OpenSCAP completa con Satellite. (Demostrativo)

Para empezar ingresamos a la sección de hosts, cumplimientos y contenidos de scap
<p align="left"><img src="../images/sat233.png?raw=true">

Creamos un nuevo contenido de SCAP
<p align="left"><img src="../images/sat234.png?raw=true">

Nombramos el nuevo contenido y seleccionamos el archivo ssg-rhel9-ds.xml descargado desde ftp://ftp.migraciones.gob.pe/openscap/ssg-rhel9-ds.xml
<p align="left"><img src="../images/sat235.png?raw=true">

Verificamos la creación del nuevo contenido
<p align="left"><img src="../images/sat236.png?raw=true">

Ahora creamos una nueva politica para el analisis completo
<p align="left"><img src="../images/sat237.png?raw=true">

Creamos una nueva politica de cumplimiento
<p align="left"><img src="../images/sat238.png?raw=true">

Marcamos la politica como Ansible
<p align="left"><img src="../images/sat239.png?raw=true">

Nombreamos la politica
<p align="left"><img src="../images/sat240.png?raw=true">

Referenciamos la politica con el contenido de openscap anterior y seleccionamos el perfil CIS Red Hat Enterprise Linux 9 Benchmark for Level 2 - Server
<p align="left"><img src="../images/sat241.png?raw=true">

Se programa el escaneo semanalmente
<p align="left"><img src="../images/sat242.png?raw=true">

Asignamos la politica al HG de PROD en RHEL9
<p align="left"><img src="../images/sat243.png?raw=true">

Verificamos la polticia de cumplimiento
<p align="left"><img src="../images/sat244.png?raw=true">

En el HG, ejecutamos los roles de ansible para ejecutar las configuraciones de openscap
<p align="left"><img src="../images/sat245.png?raw=true">

Un script de ansible realizara la configuración
<p align="left"><img src="../images/sat246.png?raw=true">

En el cliente, ejecutamos el escaneo de openscap para generar el primer reporte
<p align="left"><img src="../images/sat247.png?raw=true">

Podemos revisar el reporte completo recien creado
<p align="left"><img src="../images/sat248.png?raw=true">

Revisamos y analisamos el reporte
<p align="left"><img src="../images/sat249.png?raw=true">
<p align="left"><img src="../images/sat250.png?raw=true">


## Politica de seguridad de OpenSCAP customizada con Satellite. (Demostrativo)

La customización de perfiles se hace a traves de los tailoring file de openscap, creamos uno nuevo
<p align="left"><img src="../images/sat251.png?raw=true">

Creamos el tailoring usando el archivo ssg-rhel9-ds-aide-tailoring.xml descargado del ftp://ftp.migraciones.gob.pe/openscap/ssg-rhel9-ds-aide-tailoring.xml
<p align="left"><img src="../images/sat252.png?raw=true">

Verificamos la creación de tailoring
<p align="left"><img src="../images/sat253.png?raw=true">

Ahora creamos una nueva politica de cumplimiento customizada
<p align="left"><img src="../images/sat254.png?raw=true">

Marcamos la politica como Ansible
<p align="left"><img src="../images/sat255.png?raw=true">

Nombramos la politica como customizada
<p align="left"><img src="../images/sat256.png?raw=true">

Asociamos la politica al contenido anterior y al nuevo tailoring creado
<p align="left"><img src="../images/sat257.png?raw=true">

Tambien la definimos como de ejecucion semanal
<p align="left"><img src="../images/sat258.png?raw=true">

La asociamos al HG de PROD de RHEL9
<p align="left"><img src="../images/sat259.png?raw=true">

En el HG ejecutamos los roles de ansible
<p align="left"><img src="../images/sat260.png?raw=true">

Esperamos que el script reconfigure el HG
<p align="left"><img src="../images/sat261.png?raw=true">

En el client corremos un escaneo de openscap
<p align="left"><img src="../images/sat262.png?raw=true">

Revisamos el nuevo reporte, ahora customizado con controles especificos
<p align="left"><img src="../images/sat263.png?raw=true">

Revisamos y analizamos el nuevo reporte a detalle
<p align="left"><img src="../images/sat264.png?raw=true">

## Remediación de politica de seguridad de OpenSCAP con Satellite. (Demostrativo)

Considerando su ultimo reporte de openscap de la politica customizada
<p align="left"><img src="../images/sat265.png?raw=true">

Creamos un nuevo job para ejecutar las remediaciones
<p align="left"><img src="../images/sat266.png?raw=true">

Podemos importar la tarea de ansible con el archivo ssg-rhel9-ds-aide-tailoring.yaml descargado desde ftp://ftp.migraciones.gob.pe/openscap/ssg-rhel9-ds-aide-tailoring.yaml
<p align="left"><img src="../images/sat267.png?raw=true">

Lo grabamos en playbooks de ansible con el tipo ansible
<p align="left"><img src="../images/sat268.png?raw=true">

Programamos un trabajo en el client
<p align="left"><img src="../images/sat269.png?raw=true">

Ejecutamos el playbook de remediación
<p align="left"><img src="../images/sat270.png?raw=true">

Verificamos la correcta ejecución dl playbook
<p align="left"><img src="../images/sat271.png?raw=true">

Ejecutamos un nuevo escaneo de openscap para verificar si se ejecuto la remediación
<p align="left"><img src="../images/sat272.png?raw=true">

Revisamos el nuevo informe customizado
<p align="left"><img src="../images/sat273.png?raw=true">

Evaluamos a detalle el nuevo informe
<p align="left"><img src="../images/sat274.png?raw=true">


## Laboratorio de la unidad

<br>Con lo aprendio en clase:
<br>
<br> - Cree la politica de openscap para obtener el reporte completo de controles de seguridad completo de  CIS Red Hat Enterprise Linux 9 Benchmark for Level 2 - Server
<br> - Cree la politica de openscap para obtener el reporte customizado con el tailoring de CIS Red Hat Enterprise Linux 9 Benchmark for Level 2 - Server para controles de AIDE
<br> - Remedie los controles de aide del punto anterior y genere un nuevo reporte customizado

<p><br><a href="sat.md">volver</a></p>

