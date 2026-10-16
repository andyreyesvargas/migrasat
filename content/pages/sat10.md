<h1>Registrando Hosts de contenido</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento el procedimiento de registro de host de contenido en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de los recursos host de contenido en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Registrar un host de contenido de forma manual. (Demostrativo)
<br>- Desregistrar un host de contenido de forma manual. (Demostrativo)
<br>- Registrar un host de contenido usando llaves de activación. (Demostrativo)
<br>- Registrar un host de contenido a traves de bootstrap. (Demostrativo)
<br>- Registrar un host de contenido a traves de un script customizado. (Demostrativo)
<br>- Registrar un host de contenido a traves de script generado desde la web. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Registrar un host de contenido. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a registrar un host de contenido por el GUI de Satellite para generar un script de registro.

<p align="left"><img src="../images/sat135.png?raw=true"></p>

Ingresamos los datos de registro para un sistema del ambiente DEV en RHEL9
<p align="left"><img src="../images/sat136.png?raw=true"></p>

El sistema generara un script que podemos copiar
<p align="left"><img src="../images/sat137.png?raw=true"></p>

Con el terminal, registramos el sistema cliente
```
[root@client ~]# set -o pipefail && curl --silent --show-error  --insecure 'https://satellite.migraciones09.gob.pe/register?activation_keys=AK_DEV_RHEL9&download_utility=curl&hostgroup_id=1&location_id=2&operatingsystem_id=3&organization_id=1&update_packages=false' --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjo0LCJpYXQiOjE3OTIxNzQyNzYsImp0aSI6IjdmZGFmOTc1YWEwZDlkYjVjNDY5ZjU5NmE0M2FkYWM4YmMxNjk4MzIzNzMwNjhjYmY3NTljNGU0NDU5ZjA5YWYiLCJleHAiOjE3OTIxODg2NzYsInNjb3BlIjoicmVnaXN0cmF0aW9uI2dsb2JhbCByZWdpc3RyYXRpb24jaG9zdCJ9.j4eCj9mTx1wdSMaP4tGOH8btk2widi8z-9JtdnMo_AQ' | bash
#
# Running registration
#
subscription-manager is already installed!
The system has been registered with ID: e922637b-7d92-4db0-b916-4489ba624bdd
The registered system name is: client.migraciones09.gob.pe
# Running [client.migraciones09.gob.pe] host initial configuration
/usr/sbin/restorecon
Relabeled /root/.ssh/authorized_keys from unconfined_u:object_r:ssh_home_t:s0 to system_u:object_r:ssh_home_t:s0
#
# Installing Insights client
#
Updating Subscription Management repositories.
Waiting for process with pid 1627 to finish.
Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)            69 MB/s | 114 MB     00:01
Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)               45 MB/s | 157 MB     00:03
Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)                111 kB/s | 3.8 kB     00:00
Package insights-client-3.2.2-2.el9.noarch is already installed.
Dependencies resolved.
===================================================================================================
 Package                   Arch     Version               Repository                          Size
===================================================================================================
Upgrading:
 insights-client           noarch   3.9.3-1.el9           rhel-9-for-x86_64-appstream-rpms    55 k
 selinux-policy            noarch   38.1.75-2.el9_8.1     rhel-9-for-x86_64-baseos-rpms       41 k
 selinux-policy-targeted   noarch   38.1.75-2.el9_8.1     rhel-9-for-x86_64-baseos-rpms      6.9 M
Installing dependencies:
 insights-core             noarch   3.8.2-1.el9_8         rhel-9-for-x86_64-appstream-rpms   2.3 M
 insights-core-selinux     noarch   3.8.2-1.el9_8         rhel-9-for-x86_64-appstream-rpms    71 k

Transaction Summary
===================================================================================================
Install  2 Packages
Upgrade  3 Packages

Total download size: 9.3 M
Downloading Packages:
(1/5): insights-core-selinux-3.8.2-1.el9_8.noarch.rpm               58 kB/s |  71 kB     00:01
(2/5): insights-client-3.9.3-1.el9.noarch.rpm                       45 kB/s |  55 kB     00:01
(3/5): insights-core-3.8.2-1.el9_8.noarch.rpm                      1.7 MB/s | 2.3 MB     00:01
(4/5): selinux-policy-targeted-38.1.75-2.el9_8.1.noarch.rpm        5.3 MB/s | 6.9 MB     00:01
(5/5): selinux-policy-38.1.75-2.el9_8.1.noarch.rpm                  20 kB/s |  41 kB     00:02
---------------------------------------------------------------------------------------------------
Total                                                              2.9 MB/s | 9.3 MB     00:03
Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)           2.6 MB/s | 3.6 kB     00:00
Importing GPG key 0xFD431D51:
 Userid     : "Red Hat, Inc. (release key 2) <security@redhat.com>"
 Fingerprint: 567E 347A D004 4ADE 55BA 8A5F 199E 2F91 FD43 1D51
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
Key imported successfully
Importing GPG key 0x5A6340B3:
 Userid     : "Red Hat, Inc. (auxiliary key 3) <security@redhat.com>"
 Fingerprint: 7E46 2425 8C40 6535 D56D 6F13 5054 E4A4 5A63 40B3
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          1/1
  Preparing        :                                                                           1/1
  Upgrading        : selinux-policy-38.1.75-2.el9_8.1.noarch                                   1/8
  Running scriptlet: selinux-policy-38.1.75-2.el9_8.1.noarch                                   1/8
  Running scriptlet: selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          2/8
  Upgrading        : selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          2/8
  Running scriptlet: selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          2/8
  Running scriptlet: insights-core-selinux-3.8.2-1.el9_8.noarch                                3/8
  Installing       : insights-core-selinux-3.8.2-1.el9_8.noarch                                3/8
  Running scriptlet: insights-core-selinux-3.8.2-1.el9_8.noarch                                3/8
  Installing       : insights-core-3.8.2-1.el9_8.noarch                                        4/8
  Upgrading        : insights-client-3.9.3-1.el9.noarch                                        5/8
  Running scriptlet: insights-client-3.9.3-1.el9.noarch                                        5/8
  Running scriptlet: insights-client-3.2.2-2.el9.noarch                                        6/8
  Cleanup          : insights-client-3.2.2-2.el9.noarch                                        6/8
  Running scriptlet: insights-client-3.2.2-2.el9.noarch                                        6/8
  Running scriptlet: selinux-policy-38.1.35-2.el9_4.noarch                                     7/8
  Cleanup          : selinux-policy-38.1.35-2.el9_4.noarch                                     7/8
  Running scriptlet: selinux-policy-38.1.35-2.el9_4.noarch                                     7/8
  Cleanup          : selinux-policy-targeted-38.1.35-2.el9_4.noarch                            8/8
  Running scriptlet: selinux-policy-targeted-38.1.35-2.el9_4.noarch                            8/8
  Running scriptlet: selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          8/8
  Running scriptlet: selinux-policy-targeted-38.1.35-2.el9_4.noarch                            8/8
  Verifying        : insights-core-3.8.2-1.el9_8.noarch                                        1/8
  Verifying        : insights-core-selinux-3.8.2-1.el9_8.noarch                                2/8
  Verifying        : insights-client-3.9.3-1.el9.noarch                                        3/8
  Verifying        : insights-client-3.2.2-2.el9.noarch                                        4/8
  Verifying        : selinux-policy-38.1.75-2.el9_8.1.noarch                                   5/8
  Verifying        : selinux-policy-38.1.35-2.el9_4.noarch                                     6/8
  Verifying        : selinux-policy-targeted-38.1.75-2.el9_8.1.noarch                          7/8
  Verifying        : selinux-policy-targeted-38.1.35-2.el9_4.noarch                            8/8
Installed products updated.

Upgraded:
  insights-client-3.9.3-1.el9.noarch                   selinux-policy-38.1.75-2.el9_8.1.noarch
  selinux-policy-targeted-38.1.75-2.el9_8.1.noarch
Installed:
  insights-core-3.8.2-1.el9_8.noarch           insights-core-selinux-3.8.2-1.el9_8.noarch

Complete!
Successfully registered host client.migraciones09.gob.pe
Automatic scheduling for Insights has been enabled.
Starting to collect Insights data for client.migraciones09.gob.pe
Writing RHSM facts to /etc/rhsm/facts/insights-client.facts ...
Uploading Insights data.
Successfully uploaded report from client.migraciones09.gob.pe to account 5257369.
Refreshing subscription data
All local data refreshed
Successfully updated the system facts.
Host [client.migraciones09.gob.pe] successfully configured.
+----------------------------------------------------------+
    Available Repositories in /etc/yum.repos.d/redhat.repo
+----------------------------------------------------------+
Repo ID:   satellite-client-6-for-rhel-9-x86_64-rpms
Repo Name: Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/DEV/CV_DEV_RHEL9/content
           /dist/layered/rhel9/x86_64/sat-client/6/os
Enabled:   1

Repo ID:   rhel-9-for-x86_64-baseos-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/DEV/CV_DEV_RHEL9/content
           /dist/rhel9/9/x86_64/baseos/os
Enabled:   1

Repo ID:   rhel-9-for-x86_64-appstream-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/DEV/CV_DEV_RHEL9/content
           /dist/rhel9/9/x86_64/appstream/os
Enabled:   1
```

Podemos verificar que el sistema fue registrado
<p align="left"><img src="../images/sat138.png?raw=true"></p>

Tambien podemos verificar que una suscripción fue consumida
<p align="left"><img src="../images/sat139.png?raw=true"></p>



# Quitar el registro de un host de contenido. (Demostrativo)
Para desuscribir y borrar el registro de un host de satellite, se debe hacer en 2 partes, primero en el terminal
```
[root@client ~]# subscription-manager unregister
Unregistering from: satellite.migraciones09.gob.pe:443/rhsm
System has been unregistered.
[root@client ~]# subscription-manager remove --all
0 subscriptions removed from this system.
[root@client ~]# subscription-manager clean
All local data removed
```

El sistema aun podria aparecer en la sección de hosts en el satellite, por ello debe borrarse por el GUI tambien
<p align="left"><img src="../images/sat140.png?raw=true"></p>

Verificamos que se recupero la suscripción
<p align="left"><img src="../images/sat141.png?raw=true"></p>



# Laboratorio: 
<br>- Usando la consola web de Satellite, genere un script de registro para su cliente RHEL9 en ambiente de desarrollo
<br>- Ejecute el registro de su cliente
<br>- Verifique que el sistema esta correctamente registrado

<br>- Ejecute el registro de su cliente
<br>- Verifique que el sistema esta correctamente registrado
<br>- NO desregistre el sistema de la plataforma Satellite, lo usara para la siguiente seccion


<p><br><a href="sat">volver</a></p>
