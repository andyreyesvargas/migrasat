<h1>Gestión de paqueteria de software</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento del proceso de instalación de software desde la plataforma de Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Instalar paquetes de software en los sistemas clienteas.(Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de actualizaciones de un sistema cliente por CLI. (Demostrativo)
<br>- Gestión de actualizaciones de un sistema cliente por GUI. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Gestión de actualizaciones de un sistema cliente por CLI

Validamos la cantidad de erratas descubiertas en el servidor, tome nota de estos datos
```
[root@client ~]# yum list-security
```

Si quisieramos listar solo los RHSA
```
[root@client ~]# yum updateinfo list security
```

Podemos filtrar los RHSA por nivel de severidad
```
[root@client ~]# yum updateinfo list updates --sec-severity=Critical
[root@client ~]# yum updateinfo list updates --sec-severity=Important
[root@client ~]# yum updateinfo list updates --sec-severity=Moderate
[root@client ~]# yum updateinfo list updates --sec-severity=Low
```

Si quisieramos listar solo los RHBA
```
[root@client ~]# yum updateinfo list bugfix
```


Seleccionamos una actualizacion del tipo bugfix para corregirlas, primero examinamos la informacion detallada de la errata
```
[root@client ~]# yum updateinfo RHBA-2026:46513 --info
===============================================================================
  openssl bug fix and enhancement update
===============================================================================
  Update ID: RHBA-2026:46513
       Type: bugfix
    Updated: 2026-07-27 05:50:59
Description: OpenSSL is a toolkit that implements the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols, as well as a full-strength general-purpose cryptography library.
           :
           : Bug Fix(es) and Enhancement(s):
           :
           : * ansible-collection-microsoft-sql Connection failure: [ASN1: NOT_ENOUGH_DATA] not enough data (_ssl.c:4192) [9.8.z] (JIRA:RHEL-210862)
   Severity: None
```

Tomamos la decision de aplicar la errata
```
[root@client ~]# yum update --advisory RHBA-2026:46513
Updating Subscription Management repositories.
Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)            57 kB/s | 4.5 kB     00:00
Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)                 60 kB/s | 3.8 kB     00:00
Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)              108 kB/s | 4.1 kB     00:00
Dependencies resolved.
===================================================================================================
 Package                     Arch      Version              Repository                        Size
===================================================================================================
Upgrading:
 openssl                     x86_64    1:3.5.8-2.el9_8      rhel-9-for-x86_64-baseos-rpms    1.5 M
 openssl-fips-provider       x86_64    3.0.7-11.el9_8       rhel-9-for-x86_64-baseos-rpms     14 k
 openssl-libs                x86_64    1:3.5.8-2.el9_8      rhel-9-for-x86_64-baseos-rpms    2.3 M
Installing dependencies:
 openssl-fips-provider-so    x86_64    3.0.7-11.el9_8       rhel-9-for-x86_64-baseos-rpms    581 k

Transaction Summary
===================================================================================================
Install  1 Package
Upgrade  3 Packages

Total download size: 4.4 M
Is this ok [y/N]: y
Downloading Packages:
(1/4): openssl-fips-provider-3.0.7-11.el9_8.x86_64.rpm              12 kB/s |  14 kB     00:01
(2/4): openssl-fips-provider-so-3.0.7-11.el9_8.x86_64.rpm          413 kB/s | 581 kB     00:01
(3/4): openssl-3.5.8-2.el9_8.x86_64.rpm                            1.0 MB/s | 1.5 MB     00:01
(4/4): openssl-libs-3.5.8-2.el9_8.x86_64.rpm                       2.9 MB/s | 2.3 MB     00:00
---------------------------------------------------------------------------------------------------
Total                                                              2.2 MB/s | 4.4 MB     00:02
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                           1/1
  Installing       : openssl-fips-provider-so-3.0.7-11.el9_8.x86_64                            1/7
  Upgrading        : openssl-fips-provider-3.0.7-11.el9_8.x86_64                               2/7
  Upgrading        : openssl-libs-1:3.5.8-2.el9_8.x86_64                                       3/7
  Upgrading        : openssl-1:3.5.8-2.el9_8.x86_64                                            4/7
  Cleanup          : openssl-1:3.0.7-27.el9.x86_64                                             5/7
  Cleanup          : openssl-libs-1:3.0.7-27.el9.x86_64                                        6/7
  Cleanup          : openssl-fips-provider-3.0.7-2.el9.x86_64                                  7/7
  Running scriptlet: openssl-fips-provider-3.0.7-2.el9.x86_64                                  7/7
  Verifying        : openssl-fips-provider-so-3.0.7-11.el9_8.x86_64                            1/7
  Verifying        : openssl-fips-provider-3.0.7-11.el9_8.x86_64                               2/7
  Verifying        : openssl-fips-provider-3.0.7-2.el9.x86_64                                  3/7
  Verifying        : openssl-1:3.5.8-2.el9_8.x86_64                                            4/7
  Verifying        : openssl-1:3.0.7-27.el9.x86_64                                             5/7
  Verifying        : openssl-libs-1:3.5.8-2.el9_8.x86_64                                       6/7
  Verifying        : openssl-libs-1:3.0.7-27.el9.x86_64                                        7/7
Installed products updated.

Upgraded:
  openssl-1:3.5.8-2.el9_8.x86_64               openssl-fips-provider-3.0.7-11.el9_8.x86_64
  openssl-libs-1:3.5.8-2.el9_8.x86_64
Installed:
  openssl-fips-provider-so-3.0.7-11.el9_8.x86_64

Complete!
```

Vuelva a validar la cantidad de erratas descubiertas en el servidor y compare con el reporte anterior
```
[root@client ~]# yum updateinfo list bugfix | grep RHBA-2026:46513
```

# Gestión de actualizaciones de un sistema cliente por GUI
Desde la GUI de Satellite, ingresamos a la sección de hosts de contenido
<p align="left"><img src="../images/sat142.png?raw=true"></p>

Seleccionamos el cliente satellite
<p align="left"><img src="../images/sat143.png?raw=true"></p>

Examinamos la sección de Contenido > Errata
<p align="left"><img src="../images/sat144.png?raw=true"></p>

Podemos filtras las erratas por el tipo
<p align="left"><img src="../images/sat145.png?raw=true"></p>

Tambien filtrar por la severidad
<p align="left"><img src="../images/sat146.png?raw=true"></p>

Incluso con la combinación de tipo y severidad
<p align="left"><img src="../images/sat147.png?raw=true"></p>

Tambien con el codigo o ID de la errata
<p align="left"><img src="../images/sat148.png?raw=true"></p>

Ingresamos al codigo de la errata
<p align="left"><img src="../images/sat149.png?raw=true"></p>

Examinamos el contenido de la errata para conocer los detalles
<p align="left"><img src="../images/sat150.png?raw=true"></p>

Podemos ejecutar la aplicación de la errata seleccionándola y aplicandola
<p align="left"><img src="../images/sat151.png?raw=true"></p>

Podemos revisar como se esta ejecutando
<p align="left"><img src="../images/sat152.png?raw=true"></p>

La tarea en verde indica que se aplico de forma correcta
<p align="left"><img src="../images/sat153.png?raw=true"></p>

Si volvemos a buscar la errata con el mismo codigo, ya no deberia volver a aparecer


# Laboratorio 01: 
**NOTA: en ningun laboratorio usar el comando yum update -y, tampoco aplicar mas alla de lo solicitado**
<br>Genere los siguientes reportes en un archivo de texto 
<br> - Todos los RHSA del cliente satellite
<br> - RHSA de severidad critica del cliente satellite
<br> - RHSA de severidad importante del cliente satellite
<br> - RHSA de severidad moderada del cliente satellite
<br> - RHSA de severidad baja del cliente satellite
<br> - Todos los RHBA del cliente satellite

# Laboratorio 02: 
**NOTA: en ningun laboratorio usar el comando yum update -y, tampoco aplicar mas alla de lo solicitado**
<br>Utilizando el GUI, aplicar el RHBA-2026:46513 en el cliente satellite


# Laboratorio 03: 
**NOTA: en ningun laboratorio usar el comando yum update -y, tampoco aplicar mas alla de lo solicitado**
<br>Utilizando el CLI, aplicar el RHBA-2024:9274 en el cliente satellite


# Laboratorio 04: 
**NOTA: en ningun laboratorio usar el comando yum update -y, tampoco aplicar mas alla de lo solicitado**
<br>Utilizando el CLI o GUI, aplicar todos los RHSA de severidad critica


<p><br><a href="sat.md">volver</a></p>
