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
<br>- Ejecución de ansible roles en hosts. (Demostrativo)
<br>- Ejecución de ansible roles en host-groups. (Demostrativo)
<br>- Creación de roles de ansible. (Demostrativo)
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

## Creación de roles de ansible. (Demostrativo)

Para crear un rol de ansible ingresamos al servidor satellite y preparamos la base de directorios y archivos para crear un rol que instale el servidor ftp
```
[root@satellite ~]# cd /etc/ansible/roles/
[root@satellite roles]# ansible-galaxy init ftp-custom
- Role ftp-custom was created successfully
[root@satellite roles]# vi ftp-custom/tasks/main.yml
---
# tasks file for ftp-custom
- name: Asegurar que vsftpd esté instalado
  ansible.builtin.dnf:
     name: vsftpd
     state: present

- name: Asegurar que vsftpd esté iniciado y habilitado en el arranque
  ansible.builtin.service:
     name: vsftpd
     state: started
     enabled: true

- name: Asegurar que el cliente esté instalado
  ansible.builtin.dnf:
     name: ftp
     state: present

- name: Copiar archivo en pub
  ansible.builtin.copy:
    src: hello.txt
    dest: /var/ftp/pub/hello.txt
    mode: 644
    owner: root
    group: root

- name: Activar autenticacion anonima
  ansible.builtin.lineinfile:
    path: /etc/vsftpd/vsftpd.conf
    regexp: 'anonymous_enable=NO'
    line: 'anonymous_enable=YES'

- name: Reiniciar vsftpd
  ansible.builtin.service:
     name: vsftpd
     state: restarted

[root@satellite roles]# vi ftp-custom/files/hello.txt
FTP Migraciones
```

Ahora importamos el rol en el servidor satellite
<p align="left"><img src="../images/sat219.png?raw=true">

Seleccionamos el nuevo role ftp-custom y lo importamos
<p align="left"><img src="../images/sat220.png?raw=true">

Agregamos el role de ansible en el host client
<p align="left"><img src="../images/sat221.png?raw=true">

Aplicamos el role
<p align="left"><img src="../images/sat222.png?raw=true">

Ejecutamos el role de ansible
<p align="left"><img src="../images/sat223.png?raw=true">

Verificamos que se ejecute el role
<p align="left"><img src="../images/sat224.png?raw=true">

Podemos verificar con el terminal en el cliente que se creo el servidor FTP con una conexion local y descargando el archivo del role hello.txt
```
[root@client ~]# ftp localhost
Trying ::1...
Connected to localhost (::1).
220 (vsFTPd 3.0.5)
Name (localhost:root): ftp
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd pub
250 Directory successfully changed.
ftp> dir
229 Entering Extended Passive Mode (|||42602|)
150 Here comes the directory listing.
--w----r-T    1 0        0              16 Oct 26 16:44 hello.txt
226 Directory send OK.
ftp> get hello.txt
local: hello.txt remote: hello.txt
229 Entering Extended Passive Mode (|||13464|)
150 Opening BINARY mode data connection for hello.txt (16 bytes).
226 Transfer complete.
16 bytes received in 4.1e-05 secs (390.24 Kbytes/sec)
ftp> exit
221 Goodbye.
[root@client ~]# cat hello.txt
FTP Migraciones
```

## Laboratorio de la unidad

<br>Con lo aprendio en clase:
<br>
<br> - Cree el rol de MOTD para ejecutarlo en su client con una variable que haga referencia a su número de alumno, este rol se aplicara directamente al host
<br> - Cree el rol que permita configurar el servidor de NTP ntp.migraciones.gob.pe con roles de ansible que se aplique a todo el ambiente de PROD RHEL9(migre el sistema al ENV de PROD)
<br> - Cree y ejecute el rol customizado para crear el servidor FTP con un archivo de ejemplo

<p><br><a href="sat.md">volver</a></p>
