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
Desde la GUI de Satellite, podemos gestionar la paqueteria de software de los sistemas registrados, para ello vamos a la seccion HOST > HOSTS DE CONTENIDO
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2736.png?raw=true"width="800" height="400"></p>

Buscamos nuestro cliente RHEL8 y vemos la seccion de actualizaciones disponibles, visto de arriba hacia abajo, se muestran las actualizaciones de seguridad, correccion, mejora y paquetes.
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2737.png?raw=true"width="800" height="400"></p>

Le damos click al nombre del equipo para ingresar a las opciones
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2738.png?raw=true"width="800" height="400"></p>

Ingresamos a la seccion de ERRATA
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2739.png?raw=true"width="800" height="400"></p>

Podemos filtrar las erratas para que solo muestre las actualizaciones de seguridad
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2740.png?raw=true"width="800" height="400"></p>

Tambien podemos filtrar por severidad, en este caso las actualizaciones criticas
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2741.png?raw=true"width="800" height="400"></p>

Tambien las del nivel moderado
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2742.png?raw=true"width="800" height="400"></p>

Si quisieras ver solo las erratas de correccion
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2743.png?raw=true"width="800" height="400"></p>

De la lista anterior de bugfixes, seleccionamos la mejora de SELinux RHBA-2021:5174, le damos click al nombre de la errata para ver los detalles
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2744.png?raw=true"width="800" height="400"></p>

Analizamos la informacion de la errata y lo que involucra la actualizacion para determinar si podemos aplicarla
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2745.png?raw=true"width="800" height="400"></p>

Si tomamos la decision de aplicar la errata, la seleccionamos en la lista y la aplicamos via remote-execution
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2746.png?raw=true"width="800" height="400"></p>

La tarea deberia ejecutarse de forma correcta
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2747.png?raw=true"width="800" height="400"></p>

Volvemos a la vista de bugfixes y validamos que la actualizacion RHBA-2021:5174 ya no este disponible
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2748.png?raw=true"width="800" height="400"></p>

# Laboratorio 01: 
<br>- En su cliente RHEL8 instale el paquete firefox con el siguiente comando
```
# yum install firefox-68.6.0-1.el8_1.x86_64
```
<br>- Por la linea de comandos intente hacer un análisis, proponga y ejecute la actualización de ser necesaria para firefox. Una vez identificado el código puede utilizar:
```
# yum update --advisory=<Codigo_Identificado>
```


# Laboratorio 02: 
<br>- En su cliente RHEL8 instale el paquete vsftpd con el siguiente comando
```
# yum install vsftpd-3.0.3-28.el8.x86_64
```
<br>- Por la web de satellite intente hacer un análisis, proponga y ejecute la actualización de ser necesaria para vsftpd

# Laboratorio 03: 
<br>- En su cliente RHEL8 Verifique y aplique las erratas que sean solo de nivel CRITICO e IMPORTANTE

Solucion:
<br>
<br> **Verificar erratas**
```
# yum updateinfo list updates --sec-severity=Critical
# yum updateinfo list updates --sec-severity=Important
```

<br> **Aplicar erratas**
```
# yum update --sec-severity=Critical
# yum update --sec-severity=Important
```

<p><br><a href="sat">volver</a></p>
