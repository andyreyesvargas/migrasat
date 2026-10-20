<h1>Gestión de ejecución remota con ansible vía Red Hat Satellite</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de ejecución remota con ansible vía Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y administración de opciones de ejecución remota con ansible en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Ejecución de comandos remotos vía ansible playbooks. (Demostrativo)
<br>- Ejecución de comandos remotos vía ansible roles. (Demostrativo)
<br>- Laboratorio: Ejecución de tareas remotas con ansible playbooks y ansible roles
</p>
<p>
<strong>Laboratorios:</strong>
</p>
</p>

## Ejecución de ansible roles en hosts. (Demostrativo)

Para crear un rol de ansible a traves de Satellite, primero se debe ingresar a la sección
<p align="left"><img src="../images/sat196.png?raw=true">

Como el sistema no tiene roles cargados, ingresamos al terminal al servidor satellite y descargamos del ftp del salon el motd-role.tar.gz para enviarlo a la ruta de roles
```
[root@satellite ~]# wget ftp://ftp.migraciones.gob.pe/motd-role.tar.gz
--2026-10-19 16:22:41--  ftp://ftp.migraciones.gob.pe/motd-role.tar.gz
           => ‘motd-role.tar.gz’
motd-role.tar.gz         100%[=================================>]   1.99K  --.-KB/s    in 0s
2026-10-19 16:22:41 (116 MB/s) - ‘motd-role.tar.gz’ saved [2041]

[root@satellite ~]# tar -xzvf motd-role.tar.gz
[root@satellite ~]# mv motd /etc/ansible/roles/
```

Ahora si podemos importar el rol de ansible
<p align="left"><img src="../images/sat197.png?raw=true">

Seleccionamos el rol de motd
<p align="left"><img src="../images/sat198.png?raw=true">

La documentacion del role indica que el mensaje customizado será enviado a traves de la variables new_var, por ello ingresamos a variables
<p align="left"><img src="../images/sat199.png?raw=true">

Definimos la nueva variable
<p align="left"><img src="../images/sat200.png?raw=true">

Ingresamos los datos de la variable y a que rol estara asociado
<p align="left"><img src="../images/sat201.png?raw=true">

Verificamos la creación de la variables
<p align="left"><img src="../images/sat202.png?raw=true">

En el cliente ingresamos a la seccion de Ansible y asignamos directamente un rol
<p align="left"><img src="../images/sat203.png?raw=true">

Seleccionamos el rol motd
<p align="left"><img src="../images/sat204.png?raw=true">

Confirmamos el rol
<p align="left"><img src="../images/sat205.png?raw=true">

En los parametros agregamos la variables del tipo cadena/string con un texto que identifique nuestro equipo
<p align="left"><img src="../images/sat206.png?raw=true">

Ejecutamos los roles de Ansible
<p align="left"><img src="../images/sat207.png?raw=true">

Con la ejecución del rol, vemos si el cliente ahora cuenta con un /etc/motd con el mensaje customizado, para ello simplemente iniciamos sesión via terminal ssh
```
login as: root
root@192.168.109.11's password:
Este es un ejemplo de /etc/motd creado durante el workshop utilizando Ansible y Satellite.

Este es un ejemplo de variable new_var: Migraciones Alumno 09
Last login: Mon Oct 19 16:38:36 2026 from 192.168.109.97
```

## Ejecución de ansible roles en host-groups. (Demostrativo)

Considerando que las politicas de seguridad se aplican por ambientes o función primaria de servicios, podemos definir la ejecucion de roles por host-groups, para que sean aplicados a todos los clientes registrados en el servidor, primero preparamos los roles
<p align="left"><img src="../images/sat208.png?raw=true">

Desde el servidor satellite, importamos el rol de satellite desde el recurso ftp://ftp.migraciones.gob.pe/ansible-role-chrony.tar.gz
```
[root@satellite ~]# wget ftp://ftp.migraciones.gob.pe/ansible-role-chrony.tar.gz
--2026-10-19 21:57:13--  ftp://ftp.migraciones.gob.pe/ansible-role-chrony.tar.gz
           => ‘ansible-role-chrony.tar.gz’
ansible-role-chrony.tar. 100%[=================================>]  10.84K  --.-KB/s    in 0s
2026-10-19 21:57:13 (197 MB/s) - ‘ansible-role-chrony.tar.gz’ saved [11104]

[root@satellite ~]# tar -xzvf ansible-role-chrony.tar.gz
[root@satellite ~]# mv ansible-role-chrony /etc/ansible/roles/
```

Con el rol en la ruta de ansible, podemos importarlo a la plataforma satellite
<p align="left"><img src="../images/sat209.png?raw=true">

Seleccionamos el rol
<p align="left"><img src="../images/sat210.png?raw=true">

Ingresamos a la sección de variables
<p align="left"><img src="../images/sat211.png?raw=true">

Examinamos las posibles variables que podemos customizar en el futuro
<p align="left"><img src="../images/sat212.png?raw=true">

Ingresamos al HG de PROD de RHEL9 para aplicar el rol a todos los sistemas clientes registrados en el
<p align="left"><img src="../images/sat213.png?raw=true">

Em Ansible roles seleccionamos el role que queremos activar
<p align="left"><img src="../images/sat214.png?raw=true">

En parametros agregamos dos nuevos, uno para el pool que dejaremos en blanco y otro en server que pondremos el servidor ntp.migraciones.gob.pe
<p align="left"><img src="../images/sat215.png?raw=true">

Con el HG modificado, podemos registrar el cliente en el HG para ello generamos el script de registros
<p align="left"><img src="../images/sat216.png?raw=true">

Como el sistema ya esta registrado en otro HG, lo liberamos y re-registramos con el nuevo script
```
[root@client ~]# subscription-manager unregister
This system is currently not registered.
[root@client ~]# subscription-manager remove --all
0 subscriptions removed from this system.
[root@client ~]# subscription-manager clean
All local data removed
[root@client ~]# set -o pipefail && curl --silent --show-error  --insecure 'https://satellite.migraciones09.gob.pe/register?download_utility=curl&hostgroup_id=3&location_id=2&operatingsystem_id=3&organization_id=1&update_packages=false' --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjo0LCJpYXQiOjE3OTI0NjQ0NDcsImp0aSI6IjNjZjIwYTVhNjQ1YjVmOTcyMTEzMDkwNzBjMTExNTI0NTI0ZmJjMDY0NDQ5NDMxYzVjMmI1ZjQ1MTJjMTYzNzUiLCJleHAiOjE3OTI0Nzg4NDcsInNjb3BlIjoicmVnaXN0cmF0aW9uI2dsb2JhbCByZWdpc3RyYXRpb24jaG9zdCJ9.LzDu6rKo3yXrez2NYZ_v0l9bF3uU2jMBCpdY4MPog5U' | bash
#
# Running registration
#
subscription-manager is already installed!
The system has been registered with ID: 5fef8f8a-25f7-4d49-b034-090645468d8a
The registered system name is: client.migraciones09.gob.pe
# Running [client.migraciones09.gob.pe] host initial configuration
/usr/sbin/restorecon
#
# Installing Insights client
#
Updating Subscription Management repositories.
Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)                 78 kB/s | 3.8 kB     00:00
Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)              116 kB/s | 4.1 kB     00:00
Package insights-client-3.9.3-1.el9.noarch is already installed.
Dependencies resolved.
Nothing to do.
Complete!
This host has already been registered.
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
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/PROD/CV_PROD_RHEL9/conte
           nt/dist/layered/rhel9/x86_64/sat-client/6/os
Enabled:   1

Repo ID:   rhel-9-for-x86_64-baseos-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/PROD/CV_PROD_RHEL9/conte
           nt/dist/rhel9/9/x86_64/baseos/os
Enabled:   1

Repo ID:   rhel-9-for-x86_64-appstream-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/PROD/CV_PROD_RHEL9/conte
           nt/dist/rhel9/9/x86_64/appstream/os
Enabled:   1
```

Ahora en el HG, ejecutamos todos los roles
<p align="left"><img src="../images/sat217.png?raw=true">

Verificamos que el role se ejecute correctamente
<p align="left"><img src="../images/sat218.png?raw=true">

Podemos examinar el cliente y el status del servicio chrony
```
[root@client ~]# cat /etc/chrony.conf
# Do not manually edit this file.
# Managed by ansible-role-chrony
server ntp.migraciones.gob.pe iburst minpoll 6 maxpoll 10
bindcmdaddress 127.0.0.1
bindcmdaddress ::1
deny all
driftfile /var/lib/chrony/drift
logdir /var/log/chrony
rtcsync
makestep 1.0 3
[root@client ~]# chronyc sources
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? ntp.migraciones.gob.pe        0   7     0     -     +0ns[   +0ns] +/-    0ns
```













































Descargar en el servidor cliente la siguiente plantilla de ansible playbook
```
# wget ftp://192.168.100.203/ansible/playbook-workshop.yml
```
Inspeccionar y discutir el contenido de la plantilla.

Para generar una plantilla de ansible playbook en Red Hat Satellite ir a **Hosts > Job templates**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1035.png?raw=true">

Luego seleccionar la opción de **Nueva plantilla de trabajo**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1036.png?raw=true">

Dentro del Tab Plantilla ingresar:

* Plantilla De Trabajo|Nombre: **Custom SSH Banner**
* En el editor: Copiar y pegar el **contenido** del **playbook-workshop.yml**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1037.png?raw=true">

Dentro del tab Entradas:

* Agregar entrada

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1038.png?raw=true">

Dentro del tab Entradas ingresar:

* Template Input|Name: **banner_var**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1039.png?raw=true">

Dentro del tab Empleo ingresar:

* Categoría de trabajo: **Ansible Playbook**
* Provider Type: **Ansible**

y darle **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1040.png?raw=true">

Seleccionar dentro de **Host > Todo los hosts** el cliente correspondiente y darle click al **nombre**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1041.png?raw=true">

Seleccionar la opción de **Programar trabajo remoto**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1042.png?raw=true">

En la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Playbook**
* Plantilla de trabajo: **Custom SSH Banner**
* banner_var: **My custom ssh banner from Satellite!**

y dale click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1043.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1044.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1045.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/issue**

y darle **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1046.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1047.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1048.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/issue
My custom ssh banner from Satellite!
# cat /etc/ssh/sshd_config | grep Banner
Banner /etc/issue
```
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1049.png?raw=true">

## Ejecución de comandos remotos vía ansible roles. (Demostrativo)

Descargar en el servidor cliente la siguiente plantilla de ansible playbook
```
# wget ftp://192.168.100.203/ansible/ansible-role-motd.tgz
# tar -zxvf ansible-role-motd.tgz
```
Inspeccionar el contenido de los archivos y discutir.

Dentro del servidor satellite se puede generar un esqueleto de un ansible rol con el siguiente comando:
```
[root@satellite roles]# cd /etc/ansible/roles
[root@satellite roles]# ansible-galaxy init workshop-role
- Role workshop-role was created successfully
[root@satellite roles]# ls -l  workshop-role/
total 4
drwxr-xr-x. 2 root root   22 Apr 18 22:16 defaults
drwxr-xr-x. 2 root root    6 Apr 18 22:16 files
drwxr-xr-x. 2 root root   22 Apr 18 22:16 handlers
drwxr-xr-x. 2 root root   22 Apr 18 22:16 meta
-rw-r--r--. 1 root root 1328 Apr 18 22:16 README.md
drwxr-xr-x. 2 root root   22 Apr 18 22:16 tasks
drwxr-xr-x. 2 root root    6 Apr 18 22:16 templates
drwxr-xr-x. 2 root root   39 Apr 18 22:16 tests
drwxr-xr-x. 2 root root   22 Apr 18 22:16 vars
```

Para importar un rol utilizar las opciones **Configurar > Roles**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1050.png?raw=true">

En la pantalla de Ansible Roles darle click al botón **Import from satellite.opennova.pe**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1051.png?raw=true">

Seleccionar los roles que desee importar y darle al botón **Submit**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1052.png?raw=true">

Visualizar en la pagina de Ansible Roles que se muestren los roles seleccionados.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1053.png?raw=true">

Para importar o crear una variable de ansible seleccionar **Configurar > Variables**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1054.png?raw=true">

En la pagina de Ansible Variables seleccionar **New Ansible Variable**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1055.png?raw=true">

En la seccion de **Ansible Variable Details** ingresar la siguiente información:

* Clave De Busqueda|Clave: **new_var**
* Ansible Role: **motd**

En la seccion de Comportamiento predeterminado ingresar la siguiente información:
* Clave De Busqueda|Anular: **darle click a la casilla para activar.**
* Parameter Type: **cadena**
* Valor Predeterminado: **Bienvenido al Workshop Red Hat Satellite!**

y darle click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1056.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1057.png?raw=true">

Validar que en la pagina de **Ansible Variables**, se muestre la variable **new_var**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1058.png?raw=true">

En la opción **Hosts > Todo los hosts** seleccionar el nombre de la maquina cliente.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1059.png?raw=true">

Seleccionar la opción **Editar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1060.png?raw=true">

En el tab de **Ansible Roles** seleccionar el rol **motd**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1061.png?raw=true">

Seleccionar de la lista de **Programar trabajo remoto** la opción **Run Ansible roles**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1062.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1063.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1064.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/motd**

y le damos **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1065.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1066.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1067.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/motd
Este es un ejemplo de /etc/motd creado durante el workshop utilizando Ansible y Satellite.

Este es un ejemplo de variable enviada a través de Satellite: Bienvenido al Workshop Red Hat Satellite!
```

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1068.png?raw=true">

Si queremos que la variable no sea aplicada globalmente podemos entrar a la seccion de **Configurar > Variables**, seleccionar la variable **new_var** y en la seccion de **Comportamiento predeterminado** des-seleccionar la opción de **Clave de Busqueda|Anular** y darle click al botón enviar.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1069.png?raw=true">

Entramos a la opción de Editar de nuestro cliente y dentro del Tab de Parámetros ingresamos:

Seccion Parámetros de Host

* new_var: cadena : Bienvenido al Workshop Red Hat Satellite! - Ejecución remota Ansible Roles!

y le damos click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1070.png?raw=true">

Seleccionamos de la lista de **Programar trabajo remoto** la opción **Run Ansible Roles**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1071.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1072.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/motd**

y le damos click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1073.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1074.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1075.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/motd
Este es un ejemplo de /etc/motd creado durante el workshop utilizando Ansible y Satellite.

Este es un ejemplo de variable enviada a través de Satellite: Bienvenido al Workshop Red Hat Satellite! - Ejecucion Remota Ansible Roles!
```
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1076.png?raw=true">

### Laboratorio
1. Con el contenido de ftp://192.168.100.203/ansible/playbook-workshop.yml crear una plantilla que contenga la siguiente información:
**Pista:**
Dentro del Tab Plantilla ingresar:

* Plantilla De Trabajo|Nombre: **Custom SSH Banner User X**
* En el editor: Copiar y pegar el **contenido** del **playbook-workshop.yml**

Dentro del tab Entradas:

* Agregar entrada

Dentro del tab Entradas ingresar:

* Template Input|Name: **banner_var**

Dentro del tab Empleo ingresar:

* Categoría de trabajo: **Ansible Playbook**
* Provider Type: **Ansible**

2. Ejecutar la plantilla ansible en el cliente asignado y verificar que el banner ssh este correctamente configurado.

3. Importar el rol motd_X dentro de Red Hat Satellite, el cual deberá contener una variable con la siguiente información:
**Pista:**
En la seccion de **Ansible Variable Details** ingresar la siguiente información:

* Clave De Busqueda|Clave: **new_var**
* Ansible Role: **motd_X**

En la seccion de Comportamiento predeterminado ingresar la siguiente información:
* Clave De Busqueda|Anular: **darle click a la casilla para activar.**
* Parameter Type: **cadena**
* Valor Predeterminado: **Bienvenido al Workshop Red Hat Satellite! creado por User X**

y darle click al botón **enviar**.

4. Editar el cliente asignado y seleccionar solamente su rol motd_X y ejecutar el rol respectivo.

5. Validar vía ejecución remota y terminal que el archivo /etc/motd contenga el valor de: **Bienvenido al Workshop Red Hat Satellite! creado por User X**

<p><br><a href="sat.md">volver</a></p>
