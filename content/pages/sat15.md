<h1>Gestión de Políticas de Seguridad Openscap</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la Gestión de Políticas de Seguridad Openscap.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y administración de opciones de ejecución de Red Hat Insights (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Habilitación de Red Hat Insights en servidor Satellite. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>
</p>

## Habilitación de Red Hat Insights en servidor Satellite. (Demostrativo)

Para empezar con la integración, debemos importar algunos roles al sistema
<p align="left"><img src="../images/sat225.png?raw=true">

Seleccionamos los roles
<p align="left"><img src="../images/sat226.png?raw=true">

Ahora se puede ejecutar el proceso de registro del mismo satellite en la plataforma satellite, primero creamos un llave para la conexion del cliente
```
[root@satellite ~]# ssh-copy-id -i /usr/share/foreman-proxy/.ssh/id_rsa_foreman_proxy.pub root@satellite.migraciones09.gob.pe
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/usr/share/foreman-proxy/.ssh/id_rsa_foreman_proxy.pub"
The authenticity of host 'satellite.migraciones09.gob.pe (192.168.109.10)' can't be established.
ED25519 key fingerprint is SHA256:JzQQxCHfl4tSXyVREQq6mp0K4VQXKw+c1h+F48Dr8jc.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@satellite.migraciones09.gob.pe's password:

Number of key(s) added: 1

Now try logging into the machine, with: "ssh -i /usr/share/foreman-proxy/.ssh/id_rsa_foreman_proxy 'root@satellite.migraciones09.gob.pe'"
and check to make sure that only the key(s) you wanted were added.
```

Con la llave ssh copiada, instalamos el rpm con la config del satellite
```
[root@satellite ~]# wget https://satellite.migraciones09.gob.pe/pub/katello-ca-consumer-latest.noarch.rpm
--2026-10-27 19:30:51--  https://satellite.migraciones09.gob.pe/pub/katello-ca-consumer-latest.noarch.rpm
Resolving satellite.migraciones09.gob.pe (satellite.migraciones09.gob.pe)... 192.168.109.10
Connecting to satellite.migraciones09.gob.pe (satellite.migraciones09.gob.pe)|192.168.109.10|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10305 (10K) [application/x-rpm]
Saving to: ‘katello-ca-consumer-latest.noarch.rpm’

katello-ca-consumer-late 100%[=================================>]  10.06K  --.-KB/s    in 0s

2026-10-27 19:30:52 (93.8 MB/s) - ‘katello-ca-consumer-latest.noarch.rpm’ saved [10305/10305]

[root@satellite ~]# yum install -y katello-ca-consumer-latest.noarch.rpm
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use "rhc" or "subscription-manager" to register.

Last metadata expiration check: 0:43:26 ago on Tue 27 Oct 2026 06:47:36 PM -05.
Reading Foreman protector configuration
*** Excluded total: 7993

WARNING: Excluding 7993 packages due to foreman-protector.
Use foreman-maintain packages install/update <package>
to safely install packages without restrictions.
Use foreman-maintain upgrade run for full upgrade.

Dependencies resolved.
===================================================================================================
 Package                                               Arch      Version     Repository       Size
===================================================================================================
Installing:
 katello-ca-consumer-satellite.migraciones09.gob.pe    noarch    1.0-1       @commandline     10 k

Transaction Summary
===================================================================================================
Install  1 Package

Total size: 10 k
Installed size: 7.7 k
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                           1/1
  Installing       : katello-ca-consumer-satellite.migraciones09.gob.pe-1.0-1.noarch           1/1
  Running scriptlet: katello-ca-consumer-satellite.migraciones09.gob.pe-1.0-1.noarch           1/1
  Verifying        : katello-ca-consumer-satellite.migraciones09.gob.pe-1.0-1.noarch           1/1
Installed products updated.

Installed:
  katello-ca-consumer-satellite.migraciones09.gob.pe-1.0-1.noarch

Complete!
```

Suscribimos el servidor de forma manual
```
[root@satellite ~]# subscription-manager register
Registering to: satellite.migraciones09.gob.pe:443/rhsm
Username: admin
Password:
Hint: User "admin" is member of following organizations: apps, principal, Migraciones, operaciones
Organization: Migraciones
Hint: Organization "Migraciones" contains following environments: Library, Library/CV_DEV_RHEL9, DEV/CV_DEV_RHEL9, Library/CV_QA_RHEL9, QA/CV_QA_RHEL9, Library/CV_PROD_RHEL9, PROD/CV_PROD_RHEL9
Environments: PROD/CV_PROD_RHEL9
The system has been registered with ID: f0c688f2-207f-4fac-8042-954579fd0315
The registered system name is: satellite.migraciones09.gob.pe
```

Ahora se puede ejecutar la integración
```
[root@satellite ~]# satellite-installer --register-with-insights
2026-10-27 19:32:13 [NOTICE] [root] Loading installer configuration. This will take some time.
2026-10-27 19:32:18 [NOTICE] [root] Running installer with log based terminal output at level NOTICE.
2026-10-27 19:32:18 [NOTICE] [root] Use -l to set the terminal output log level to ERROR, WARN, NOTICE, INFO, or DEBUG. See --full-help for definitions.
2026-10-27 19:32:19 [NOTICE] [checks] System checks passed
Package versions are locked. Continuing with unlock.
2026-10-27 19:32:26 [NOTICE] [configure] Starting system configuration.
2026-10-27 19:32:38 [NOTICE] [configure] 250 configuration steps out of 1546 steps complete.
2026-10-27 19:32:39 [NOTICE] [configure] 500 configuration steps out of 1549 steps complete.
2026-10-27 19:32:44 [NOTICE] [configure] 750 configuration steps out of 1551 steps complete.
2026-10-27 19:32:45 [NOTICE] [configure] 1000 configuration steps out of 1557 steps complete.
2026-10-27 19:32:45 [NOTICE] [configure] 1250 configuration steps out of 1557 steps complete.
2026-10-27 19:33:42 [NOTICE] [configure] 1500 configuration steps out of 1557 steps complete.
2026-10-27 19:33:45 [NOTICE] [configure] System configuration has finished.
2026-10-27 19:33:45 [NOTICE] [post] Registering the system with Red Hat Insights
  Success!
  * Satellite is running at https://satellite.migraciones09.gob.pe

  * Satellite is registered with Insights at Successfully uploaded report from satellite.migraciones09.gob.pe to account 5257369.

  * To install an additional Capsule on separate machine continue by running:

      capsule-certs-generate --foreman-proxy-fqdn "$CAPSULE" --certs-tar "/root/$CAPSULE-certs.tar"
  * Capsule is running at https://satellite.migraciones09.gob.pe:9090

The full log is at /var/log/foreman-installer/satellite.log
Package versions are being locked.
```

En las opciones de satellite, elegimos Ligthspeed que seria el nuevo insigths
<p align="left"><img src="../images/sat227.png?raw=true">

Con el boton de configurar, reconfiguramos la integración
<p align="left"><img src="../images/sat228.png?raw=true">

Una tarea de ansible verificara que se ejecuto el proceso
<p align="left"><img src="../images/sat229.png?raw=true">

Regresamos a subir inventario y sincronizamos contenido
<p align="left"><img src="../images/sat230.png?raw=true">

En el cliente, podemos hacer algunas operaciones de verificación
```
[root@client ~]# insights-client --diagnosis
{"id": "f974f0da-ba73-4d66-b53a-d01be67d0461", "insights_id": "e922637b-7d92-4db0-b916-4489ba624bdd", "details": {"hardening_http_marked_insecure|HARDENING_HTTPS_DISABLED_WEBSERVER": {"rpm": "httpd-2.4.62-13.el9_8.6", "conf": {"filepath": "/etc/httpd/conf/httpd.conf", "nssengine": null, "sslengine": null, "crtkeyfile": null}, "rhel": 9, "type": "rule", "service": "httpd", "error_key": "HARDENING_HTTPS_DISABLED_WEBSERVER"}, "hardening_vsftpd_banner_not_configured|VSFTPD_BANNER_NOT_CONFIGURED_V2": {"rhel": "9.4", "type": "rule", "error_key": "VSFTPD_BANNER_NOT_CONFIGURED_V2"}, "insights_client_core_collection|COLLECTION_ISSUE": {"rpm": true, "rhel": "9.4", "type": "rule", "error_key": "COLLECTION_ISSUE"}, "grub_default_file_missing_or_invalid|GRUB_DEFAULT_FILE_MISSING_OR_INVALID": {"type": "rule", "is_empty": false, "rhel_ver": "9.4", "error_key": "GRUB_DEFAULT_FILE_MISSING_OR_INVALID", "grub_file": "/etc/default/grub", "is_missing": false, "boot_device": "nvme0n1p2", "missing_cmdline": false}}}
[root@client ~]# insights-client --test
GET https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/v1/branch_info
HTTP Status: 200 OK
HTTP Response Text: {"remote_leaf":"5fef8f8a-25f7-4d49-b034-090645468d8a","remote_branch":"9dce1305-eef3-4500-b034-145cc9ac756a","display_name":"Migraciones","hostname":"satellite.migraciones09.gob.pe","product":{"type":"Satellite","major_version":"6","minor_version":"18"},"organization_id":1,"satellite_instance_id":"bf1c9ba3-da94-4334-9955-2efc4281258d","labels":[{"namespace":"satellite","key":"location","value":"Lima"},{"namespace":"satellite","key":"location","value":"Lima"},{"namespace":"satellite","key":"hostgroup","value":"HG_PROD_RHEL9"},{"namespace":"satellite","key":"hostgroup","value":"HG_PROD_RHEL9"},{"namespace":"satellite","key":"organization","value":"Migraciones"},{"namespace":"satellite","key":"organization_label","value":"Migraciones"},{"namespace":"satellite","key":"lifecycle_environment","value":"PROD"},{"namespace":"satellite","key":"activation_key","value":"AK_PROD_RHEL9"},{"namespace":"satellite","key":"content_view","value":"CV_PROD_RHEL9"},{"namespace":"satellite","key":"satellite_instance_id","value":"bf1c9ba3-da94-4334-9955-2efc4281258d"},{"namespace":"satellite","key":"organization_id","value":"1"}]}
Running Connection Tests...
=== Begin Upload URL Connection Test ===
Testing: https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/uploads/
POST https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/uploads/ data={'test': 'test'}
HTTP Status: 200 OK
HTTP Response Text: {"request_id":"55583b29b6104a1dae5d8fce21a4c61e","upload":{"account_number":"5257369","org_id":"6167305"}}
Successfully connected to: https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/uploads/
=== End Upload URL Connection Test: SUCCESS ===

=== Begin API URL Connection Test ===
Testing: https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/
GET https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/
HTTP Status: 200 OK
HTTP Response Text: {"status":"available"}
Successfully connected to: https://satellite.migraciones09.gob.pe:443/redhat_access/r/insights/
=== End API URL Connection Test: SUCCESS ===

Connectivity tests completed successfully
See /var/log/insights-client/insights-client.log for more details.
```

Como el cliente si esta conectado al insigths del satellite y esta recibiendo inventario, podemos realizar las operaciones de verificación y remediación
<p align="left"><img src="../images/sat231.png?raw=true">

Seleccionamos un recomendación y elegimos aplicarla despues de un analisis
<p align="left"><img src="../images/sat232.png?raw=true">

Algunas remediaciones serian manuales, otras con playbooks autogenerados por Satellite, incluso algunas implican reinicios, utilice sus criterios para aplicar estas remediaciones

## Laboratorio de la unidad

<br>Con lo aprendio en clase:
<br>
<br> - Active la integración de Satellite con Insigths para remediar algunas recomendaciones disponibles para su cliente RHEL9

<p><br><a href="sat.md">volver</a></p>
