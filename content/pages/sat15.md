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

## Backup y Restore de Satellite. (Demostrativo)
Realice un backup offline de la plataforma, no es necesario respaldar el contenido de pulp ya que puede ser resincronizado desde la web de redhat
```
[root@satellite ~]# mkdir /var/backup
[root@satellite ~]# satellite-maintain backup offline --skip-pulp-content /var/backup
Starting backup: 2026-10-28 16:37:22 -0500
Running preparation steps required to run the next scenarios
================================================================================
Make sure Foreman DB is up:
/ Checking connection to the Foreman DB                               [OK]
--------------------------------------------------------------------------------
Make sure Candlepin DB is up:
\ Checking connection to the Candlepin DB                             [OK]
--------------------------------------------------------------------------------
Make sure Pulpcore DB is up:
- Checking connection to the Pulpcore DB                              [OK]
--------------------------------------------------------------------------------


Running Backup
================================================================================
Make sure Foreman DB indexes are OK:                                  [OK]
--------------------------------------------------------------------------------
Make sure Candlepin DB indexes are OK:                                [OK]
--------------------------------------------------------------------------------
Make sure Pulpcore DB indexes are OK:                                 [OK]
--------------------------------------------------------------------------------
Check for running tasks:                                              [OK]
--------------------------------------------------------------------------------
Check for running pulpcore tasks:                                     [OK]
--------------------------------------------------------------------------------
Confirm turning off services is allowed:
WARNING: This script will stop your services.

Do you want to proceed?, [y(yes), q(quit)] y
                                                                      [OK]
--------------------------------------------------------------------------------
Prepare backup Directory:
Creating backup folder /var/backup/satellite-backup-2026-10-28-16-37-22
                                                                      [OK]
--------------------------------------------------------------------------------
Generate metadata:
| Saving metadata to metadata.yml                                     [OK]
--------------------------------------------------------------------------------
Detect features available in the local proxy:                         [OK]
--------------------------------------------------------------------------------
Stop applicable services:

Stopping the following service(s):
redis, postgresql, pulpcore-api, pulpcore-content, pulpcore-worker@1.service, pulpcore-worker@2.service, tomcat, pulpcore-api.socket, pulpcore-content.socket, dynflow-sidekiq@orchestrator, foreman, httpd, foreman.socket, dynflow-sidekiq@worker-1, dynflow-sidekiq@worker-hosts-queue-1, foreman-proxy
| All services stopped                                                [OK]
--------------------------------------------------------------------------------
Backup config files:
- Collecting config files to backup                                   [OK]
--------------------------------------------------------------------------------
Backup Pulp data:                                                     [SKIPPED]
--------------------------------------------------------------------------------
Start applicable services:

Starting the following service(s):
postgresql
\ All services started                                                [OK]
--------------------------------------------------------------------------------
Backup Candlepin database:
\ Getting Candlepin DB dump                                           [OK]
--------------------------------------------------------------------------------
Backup Foreman database:
- Getting Foreman DB dump                                             [OK]
--------------------------------------------------------------------------------
Backup Pulpcore database:
\ Getting Pulpcore DB dump                                            [OK]
--------------------------------------------------------------------------------
Start applicable services:

Starting the following service(s):
redis, postgresql, pulpcore-api, pulpcore-content, pulpcore-worker@1.service, pulpcore-worker@2.service, tomcat, dynflow-sidekiq@orchestrator, foreman, httpd, dynflow-sidekiq@worker-1, dynflow-sidekiq@worker-hosts-queue-1, foreman-proxy
| All services started                                                [OK]
--------------------------------------------------------------------------------
Compress backup data to save space:                                   [OK]
--------------------------------------------------------------------------------

Done with backup: 2026-10-28 16:40:53 -0500
**** BACKUP Complete, contents can be found in: /var/backup/satellite-backup-2026-10-28-16-37-22 ****
```

Borramos algun elemento de satellite como los informes de openscap

Restauramos la plataforma tomando como referencia el ultimo backup
```
[root@satellite ~]# satellite-maintain restore /var/backup/satellite-backup-2026-10-28-16-37-22
Running preparation steps required to run the next scenarios
================================================================================
Make sure Candlepin DB is up:
/ Checking connection to the Candlepin DB                             [OK]
--------------------------------------------------------------------------------
Make sure Foreman DB is up:
- Checking connection to the Foreman DB                               [OK]
--------------------------------------------------------------------------------
Make sure Pulpcore DB is up:
- Checking connection to the Pulpcore DB                              [OK]
--------------------------------------------------------------------------------


Running Restore backup
================================================================================
Check if command is run as root user:                                 [OK]
--------------------------------------------------------------------------------
Validate backup has appropriate files:                                [OK]
--------------------------------------------------------------------------------
Validate hostname is the same as backup:                              [OK]
--------------------------------------------------------------------------------
Validate network interfaces match the backup:                         [OK]
--------------------------------------------------------------------------------
Validate permissions for PostgreSQL dumps:                            [OK]
--------------------------------------------------------------------------------
Confirm dropping databases and running restore:

WARNING: This script will drop and restore your database.
Your existing installation will be replaced with the backup database.
Once this operation is complete there is no going back.
Do you want to proceed?, [y(yes), q(quit)] y
                                                                      [OK]
--------------------------------------------------------------------------------
Ensure required packages are installed before restore:                [OK]
--------------------------------------------------------------------------------
Restore configs from backup:
/ Restoring configs                                                   [OK]
--------------------------------------------------------------------------------
Stop cron service:

Stopping the following service(s):
crond
/ All services stopped                                                [OK]
--------------------------------------------------------------------------------
Run installer reset:
/ Installer reset                                                     [OK]
--------------------------------------------------------------------------------
Stop applicable services:

Stopping the following service(s):
redis, postgresql, pulpcore-api, pulpcore-content, pulpcore-worker@1.service, pulpcore-worker@2.service, tomcat, pulpcore-api.socket, pulpcore-content.socket, dynflow-sidekiq@orchestrator, foreman, httpd, foreman.socket, dynflow-sidekiq@worker-1, dynflow-sidekiq@worker-hosts-queue-1, foreman-proxy
\ All services stopped                                                [OK]
--------------------------------------------------------------------------------
Drop postgresql databases:
/ Dropping pulpcore database                                          [OK]
--------------------------------------------------------------------------------
Start applicable services:

Starting the following service(s):
postgresql
- All services started                                                [OK]
--------------------------------------------------------------------------------
Restore candlepin postgresql dump from backup:
\ Restoring candlepin dump                                            [OK]
--------------------------------------------------------------------------------
Restore foreman postgresql dump from backup:
| Restoring foreman dump                                              [OK]
--------------------------------------------------------------------------------
Restore pulpcore postgresql dump from backup:
\ Restoring pulpcore dump                                             [OK]
--------------------------------------------------------------------------------
Stop applicable services:

Stopping the following service(s):
postgresql
- All services stopped                                                [OK]
--------------------------------------------------------------------------------
Running satellite-installer :                                         [OK]
--------------------------------------------------------------------------------
Execute upgrade:run rake task:                                        [OK]
--------------------------------------------------------------------------------
Start cron service:

Starting the following service(s):
crond
- All services started                                                [OK]
--------------------------------------------------------------------------------
```


<p><br><a href="sat.md">volver</a></p>

