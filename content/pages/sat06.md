<h1>Entendimiento y gestión de usuarios</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de organizaciones y ubicaciones en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de Organizaciones y Ubicaciones en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Crear Usuarios en Satellite por GUI. (Demostrativo)
<br>- Crear Usuarios en Satellite por CLI hammer. (Demostrativo)
<br>- Crear Grupos en Satellite por GUI. (Demostrativo)
<br>- Crear Grupos en Satellite por CLI hammer. (Demostrativo)
<br>- Crear Roles en Satellite por GUI. (Demostrativo)
<br>- Crear Roles en Satellite por CLI hammer. (Demostrativo)
<br>- Laboratorio: Creando usuarios, grupos y roles en Red Hat Satellite por GUI y CLI
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Crear usuarios en Satellite por GUI. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a crear usuarios por la herramienta gráfica.

**Administrar > Usuarios**

<p align="left"><img src="../images/sat27.png?raw=true"width="800" height="400"></p>

En la pagina de Usuarios darle click al boton **Crear usuario**

<p align="left"><img src="../images/sat28.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="../images/sat29.png?raw=true"width="800" height="400"></p>

Verificar que el nuevo usuario se haya creado de manera satisfactoria en la pagina **Usuarios**

<p align="left"><img src="../images/sat30.png?raw=true"width="800" height="400"></p>

Seleccionar en la lista de la **columna acciones** la opción **Impersonate** para validar los accesos efectivos

<p align="left"><img src="../images/sat31.png?raw=true"width="800" height="400"></p>

Verificar que se ha cambiado al usuario temporalmente de manera satisfactoria

<p align="left"><img src="../images/sat32.png?raw=true"width="800" height="400"></p>

Marcar el símbolo de Impersonate y confirmar para salir del modo

<p align="left"><img src="../images/sat33.png?raw=true"width="800" height="400"></p>

Hacer click en el **nombre del usuario** para modificar sus propiedades y adicionarle el **rol de administrador**

<p align="left"><img src="../images/sat34.png?raw=true"width="800" height="400"></p>

Dentro del las opciones de **roles** marcar la **casilla de Administrador** y presionar el botón **Enviar**

<p align="left"><img src="../images/sat35.png?raw=true"width="800" height="400"></p>

Verificar que el usuario ahora tenga en la **columna Administrador** el check **activado**.

<p align="left"><img src="../images/sat36.png?raw=true"width="800" height="400"></p>

Salir temporalmente de la cuenta de administrador para validar el acceso a nivel administrador para el usuario

<p align="left"><img src="../images/sat37.png?raw=true"width="800" height="400"></p>

Ingresar las credenciales

<p align="left"><img src="../images/sat38.png?raw=true"width="800" height="400"></p>

Validar el acceso y rol Administrador

<p align="left"><img src="../images/sat39.png?raw=true"width="800" height="400"></p>

# Crear usuarios en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear usuario con los datos que se muestran en la siguiente salida.

```
[root@satellite ~]# hammer user create --login andy.reyes --firstname Andy --lastname Reyes --mail andy.reyes@opennova.pe --default-organization 'Migraciones' --default-location 'Lima' --password redhat --auth-source 'Internal' --admin true
User [andy.reyes] created.
```
NOTA: Para identificar la información de organización,ubicación y fuente de autenticación utilizar las salidas indicadas.
```
[root@satellite ~]# hammer organization list
---|--------------|--------------|-------------------------------------|------------
ID | TITLE        | NAME         | DESCRIPTION                         | LABEL
---|--------------|--------------|-------------------------------------|------------
7  | Aplicaciones | Aplicaciones | Servidores del área de aplicaciones | apps
3  | Global Bank  | Global Bank  | Organizacion Principal              | principal
1  | Migraciones  | Migraciones  |                                     | Migraciones
---|--------------|--------------|-------------------------------------|------------
[root@satellite ~]# hammer location list
---|------------|------------|--------------------
ID | TITLE      | NAME       | DESCRIPTION
---|------------|------------|--------------------
2  | Lima       | Lima       |
5  | Panama     | Panama     | Sede Principal
8  | San Isidro | San Isidro | Data Center Level 3
---|------------|------------|--------------------

[root@satellite ~]# hammer auth-source list
---|----------|--------------------
ID | NAME     | TYPE OF AUTH SOURCE
---|----------|--------------------
1  | Internal | AuthSourceInternal
3  | External | AuthSourceExternal
---|----------|--------------------
```

Listar los usuarios para validar
```
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | DISABLED | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
4  | admin         | Admin User    | root@migraciones09.gob.pe | yes   | no       | 2026/10/13 16:02:10 | Internal
7  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   | no       |                     | Internal
6  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | no       | 2026/10/07 21:42:03 | Internal
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
```

Autenticarse por linea de comandos con el usuario andy.reyes y realizar consultas.
```
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat
Successfully logged in as 'andy.reyes'.
[root@satellite ~]# hammer organization list
---|--------------|--------------|-------------------------------------|------------
ID | TITLE        | NAME         | DESCRIPTION                         | LABEL
---|--------------|--------------|-------------------------------------|------------
7  | Aplicaciones | Aplicaciones | Servidores del área de aplicaciones | apps
3  | Global Bank  | Global Bank  | Organizacion Principal              | principal
1  | Migraciones  | Migraciones  |                                     | Migraciones
---|--------------|--------------|-------------------------------------|------------
[root@satellite ~]# hammer location list
---|------------|------------|--------------------
ID | TITLE      | NAME       | DESCRIPTION
---|------------|------------|--------------------
2  | Lima       | Lima       |
5  | Panama     | Panama     | Sede Principal
8  | San Isidro | San Isidro | Data Center Level 3
---|------------|------------|--------------------
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | DISABLED | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
4  | admin         | Admin User    | root@migraciones09.gob.pe | yes   | no       | 2026/10/13 16:02:10 | Internal
7  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   | no       | 2026/10/13 16:06:29 | Internal
6  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | no       | 2026/10/07 21:42:03 | Internal
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
```

Validar el acceso por GUI

<p align="left"><img src="../images/sat40.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="../images/sat41.png?raw=true"width="800" height="400"></p>

Actualizar la contraseña del usuario andy.reyes
```
[root@satellite ~]# hammer user update --password redhat123 --login andy.reyes
[Foreman] Username: andy.reyes
[Foreman] Password for andy.reyes:
User [andy.reyes] updated.
```
Validar que ahora acepte la nueva contraseña
```
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat
Invalid credentials, continuing with session for 'andy.reyes'.
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat123
Successfully logged in as 'andy.reyes'.
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | DISABLED | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
4  | admin         | Admin User    | root@migraciones09.gob.pe | yes   | no       | 2026/10/13 16:02:10 | Internal
7  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   | no       | 2026/10/13 16:15:28 | Internal
6  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | no       | 2026/10/07 21:42:03 | Internal
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
```

Borrar el usuario andy.reyes
```
[root@satellite ~]# hammer user delete --login andy.reyes
Could not delete the user:
  Access denied
  You are trying to delete your own account
[root@satellite ~]# hammer auth login basic --username admin --password redhat
Successfully logged in as 'admin'.
[root@satellite ~]# hammer user delete --login andy.reyes
User [andy.reyes] deleted.
```
Listar los usuarios para validar
```
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | DISABLED | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
4  | admin         | Admin User    | root@migraciones09.gob.pe | yes   | no       | 2026/10/13 16:16:36 | Internal
6  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | no       | 2026/10/07 21:42:03 | Internal
---|---------------|---------------|---------------------------|-------|----------|---------------------|--------------
```

# Crear Grupos de usuarios en Satellite por GUI. (Demostrativo)
**Administrar > Grupos de usuario**

<p align="left"><img src="../images/sat42.png?raw=true"width="800" height="400"></p>

En la pagina de Grupos de usuario darle click al botón **Crear grupos de usuario**

<p align="left"><img src="../images/sat43.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="../images/sat44.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="../images/sat45.png?raw=true"width="800" height="400"></p>

Verificar y editar el grupo de usuarios

<p align="left"><img src="../images/sat46.png?raw=true"width="800" height="400"></p>

En la opción de **roles** seleccionar la **casilla de Administrar** y darle al botón **Enviar**

<p align="left"><img src="../images/sat47.png?raw=true"width="800" height="400"></p>

# Crear Grupos de usuario en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear el grupo de usuario dba_admins con los datos que se muestran en la siguiente salida.
```
[root@satellite ~]# hammer user create --login andy.reyes --firstname Andy --lastname Reyes --mail andy.reyes@opennova.pe --default-organization 'Migraciones' --default-location 'Lima' --password redhat --auth-source 'Internal' --admin true
User [andy.reyes] created.

[root@satellite ~]# hammer user-group create --name dba_admins --admin true --users andy.reyes
User group [dba_admins] created.
```
Listar los grupos de usuario para validar
```
[root@satellite ~]# hammer user-group list
---|------------|------
ID | NAME       | ADMIN
---|------------|------
1  | apps_admin | no
2  | dba_admins | yes
---|------------|------
```
Listar la información del grupo de usuario dba_admins

```
[root@satellite ~]# hammer user-group info --name dba_admins
Id:                   2
Name:                 dba_admins
Admin:                yes
Users:
    andy.reyes
User groups:

External user groups:

Roles:

Created at:           2026/10/13 16:40:04
Updated at:           2026/10/13 16:40:04
```
Listar la información del usuario y verificar que tiene el grupo asociado
```
[root@satellite ~]# hammer user info --login andy.reyes
Id:                    9
Login:                 andy.reyes
Name:                  Andy Reyes
Email:                 andy.reyes@opennova.pe
Admin:                 yes
Disabled:              no
Last login:
Authorized by:         Internal
Email enabled:         no
Effective admin:       yes
Locale:                default
Timezone:              default
Description:
Default organization:  Migraciones
Default location:      Lima
Roles:

User groups:
 1) Usergroup: dba_admins
    Roles:
Inherited User groups:

Created at:            2026/10/13 16:39:44
Updated at:            2026/10/13 16:39:44
```

Agregar un nuevo usuario al grupo dba_admins
```
[root@satellite ~]# hammer user-group add-user --user jaime.zamudio --name dba_admins
The user has been associated.
[root@satellite ~]# hammer user-group info --name dba_admins
Id:                   2
Name:                 dba_admins
Admin:                yes
Users:
    andy.reyes
    jaime.zamudio
User groups:

External user groups:

Roles:

Created at:           2026/10/13 16:40:04
Updated at:           2026/10/13 16:40:04
```

Modificar el nombre del grupo de usuarios a dbas_admin
```
[root@satellite ~]# hammer user-group update --name dba_admins --new-name dbas_admins
User group [dbas_admins] updated.
[root@satellite ~]# hammer user-group list
---|-------------|------
ID | NAME        | ADMIN
---|-------------|------
1  | apps_admin  | no
2  | dbas_admins | yes
---|-------------|------
[root@satellite ~]# hammer user-group info --name dbas_admins
Id:                   2
Name:                 dbas_admins
Admin:                yes
Users:
    andy.reyes
    jaime.zamudio
User groups:

External user groups:

Roles:

Created at:           2026/10/13 16:40:04
Updated at:           2026/10/13 16:43:22
```


Borrar el grupo de usuarios **dbas_admin**
```
[root@satellite ~]# hammer user-group delete --name dbas_admins
User group [dbas_admins] deleted.
```
Listar el grupo de usuario para validar
```
[root@satellite ~]# hammer user-group list
---|------------|------
ID | NAME       | ADMIN
---|------------|------
1  | apps_admin | no
---|------------|------
```
# Crear Roles en Satellite por GUI. (Demostrativo)
**Administrar > Roles**

<p align="left"><img src="../images/sat48.png?raw=true"width="800" height="400"></p>

En la pagina de Roles darle click al botón **Crear rol**

<p align="left"><img src="../images/sat49.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al botón **Enviar**

<p align="left"><img src="../images/sat50.png?raw=true"width="800" height="400"></p>

Verificar que el rol se haya creado de manera satisfactoria y darle click al botón **Filtros**

<p align="left"><img src="../images/sat51.png?raw=true"width="800" height="400"></p>

En la pagina de filtros darle click al botón **Crear filtro**

<p align="left"><img src="../images/sat52.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al botón **Enviar**

<p align="left"><img src="../images/sat53.png?raw=true"width="800" height="400"></p>

Verificar que el filtro se haya creado de manera satisfactoria

<p align="left"><img src="../images/sat54.png?raw=true"width="800" height="400"></p>

Validar en el perfil de un usuario si en la opción de **roles** ahora se pueda buscar el rol Application Admins como muestra la imagen

<p align="left"><img src="../images/sat55.png?raw=true"width="800" height="400"></p>

# Crear Roles en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear el rol **Database Admins** con los datos que se muestran en la siguiente salida.
```
[root@satellite ~]# hammer role create --name 'Database Admins' --description 'Administradores de Base de Datos' --organization 'Migraciones' --location 'Lima'
User role [Database Admins] created.
```
Listar los roles para validar
```
[root@satellite ~]# hammer role list
---|--------------------------------|--------
ID | NAME                           | BUILTIN
---|--------------------------------|--------
16 | Ansible Roles Manager          | no
17 | Ansible Tower Inventory Reader | no
33 | Application Admins             | no
11 | Auditor                        | no
10 | Bookmarks manager              | no
18 | Boot disk access               | no
22 | Compliance manager             | no
21 | Compliance viewer              | no
26 | Content Exporter               | no
25 | Content Importer               | no
23 | Create ARF report              | no
34 | Database Admins                | no
1  | Default role                   | yes
20 | Discovery Manager              | no
19 | Discovery Reader               | no
7  | Edit hosts                     | no
5  | Edit partition tables          | no
27 | ForemanRhCloud                 | no
2  | Manager                        | no
3  | Organization admin             | no
24 | Register hosts                 | no
15 | Remote Execution Manager       | no
14 | Remote Execution User          | no
9  | Site manager                   | no
4  | System admin                   | no
12 | Tasks Manager                  | no
13 | Tasks Reader                   | no
8  | Viewer                         | no
6  | View hosts                     | no
29 | Virt-who Manager               | no
28 | Virt-who Reporter              | no
30 | Virt-who Viewer                | no
32 | Webhooks Manager               | no
31 | Webhooks Reader                | no
---|--------------------------------|--------
```
También se puede simplificar la vista con el siguiente comando
```
[root@satellite ~]# hammer role list --search 'Database Admins'
---|-----------------|--------
ID | NAME            | BUILTIN
---|-----------------|--------
33 | Database Admins | no
---|-----------------|--------
```
Listar el permiso **access dashboard**
```
[root@satellite ~]# hammer filter available-permissions --search 'access_dashboard'
---|-----------------|--------
ID | NAME            | BUILTIN
---|-----------------|--------
34 | Database Admins | no
---|-----------------|--------

```
Asociar permiso **access_dashboard** a rol **Database Admins**
```
[root@satellite ~]# hammer filter create --permissions 'access_dashboard' --role 'Database Admins'
```

Listar el filtro asociado al rol 'Database Admins'
```
[root@satellite ~]# hammer filter list --search 'Database Admins'
----|-----------------|--------|------------|-----------|-----------------|-----------------
ID  | RESOURCE TYPE   | SEARCH | UNLIMITED? | OVERRIDE? | ROLE            | PERMISSIONS
----|-----------------|--------|------------|-----------|-----------------|-----------------
326 | (Miscellaneous) | none   | yes        | no        | Database Admins | access_dashboard
----|-----------------|--------|------------|-----------|-----------------|-----------------
```
Crear el usuario 'dbasuser'
```
[root@satellite ~]# hammer user create --login dbasuser --auth-source 'Internal' --mail dbasuser@opennova.pe --password redhat
```
Asignar el rol 'Database Admins' al usuario 'dbasuser'
```
[root@satellite ~]# hammer user add-role --role 'Database Admins' --login 'dbasuser'
```


Modificar el nombre del rol 'Database Admins' a 'Oracle Database Admins'
```
[root@satellite ~]# hammer role update --new-name 'Oracle Database Admins' --name 'Database Admins'
User role [Oracle Database Admins] updated.
```

Validamos que el cambio conserve el permiso **access_dashboard** hacia el rol **'Oracle Database Admins'**
```
[root@satellite ~]# hammer filter list --search 'Oracle Database Admins'
----|-----------------|--------|------------|-----------|------------------------|-----------------
ID  | RESOURCE TYPE   | SEARCH | UNLIMITED? | OVERRIDE? | ROLE                   | PERMISSIONS
----|-----------------|--------|------------|-----------|------------------------|-----------------
326 | (Miscellaneous) | none   | yes        | no        | Oracle Database Admins | access_dashboard
----|-----------------|--------|------------|-----------|------------------------|-----------------
```
Borrar el rol 'Oracle Database Admins'
```
[root@satellite ~]# hammer role delete --name 'Oracle Database Admins'
User role [Oracle Database Admins] deleted.
```
# Laboratorio de la Unidad
<br>El siguiente laboratorio se realizara en el servidor Satellite instalado en el capitulo anterior
### <br>**1. Crear un usuario, grupo y rol utilizando la GUI**
<br>**Crear una usuario con los siguiente datos:**
<br>
<br>**-** Login: **appsuser** 
<br>**-** Nombre: Administrador
<br>**-** Apellido: Aplicaciones
<br>**-** Correo: appsuser@redhat.com
<br>**-** Autorizado por: INTERNAL
<br>**-** Contraseña: redhat
<br>**-** Verificar: redhat
<br>**-** Organizacion y Ubicacion: Default
<br>**-** Habilitar al usuario como Administrador de Satellite.

<br>**Crear un grupo de usuarios con los siguiente datos:**
<br>
<br>**-** Nombre: **apps_admins**
<br>**-** Asociar el usuario appsuser al grupo apps_admins
<br>**-** Marcar al grupo como administrador
<br> 

<br>**Crear un rol con los siguiente datos:**
<br>
<br>**-** Nombre: **Application Admins**
<br>**-** Ubicacion y Organizacion: Default Location, Default Organization
<br>**-** Aplicar el filtro de access_dashboard
<br>**-** Asociar el rol al usuario appsuser
<br>

### 2. Crear un usuario, grupo y rol utilizando la CLI hammer.
<br>**Crear un usuario con los siguiente datos:**
<br>
<br> **-** Login: **dbasuser** 
<br> **-** Nombre: Administrador
<br> **-** Apellido: Base de Datos
<br> **-** Correo: dbauser@redhat.com
<br> **-** Autorizado por: INTERNAL
<br> **-** Contraseña: redhat
<br> **-** Verificar: redhat
<br> **-** Organizacion y Ubicacion: Default (usar --organization y --location)
<br> **-** Habilitar al usuario como Administrador de Satellite.

<br>Solucion:
```
[root@satellite ~]# hammer user create --login dbauser --firstname DBA --lastname Admin --mail dbauser@redhat.com --organization 'Default Organization' --location 'Default Location' --password redhat --auth-source 'Internal'
```

<br>**Crear un grupo de usuarios con los siguiente datos:**
<br>
<br>**-** Nombre: **dbas_admins**
<br>**-** Asociar el usuario dbasuser al grupo dbas_admins
<br>**-** Marcar al grupo como administrador
<br> 
Solucion:
```
[root@satellite ~]# hammer user-group create --name dbas_admins --roles "Auditor" --users dbauser
```

<br>**Crear un rol con los siguiente datos:**
<br>
<br>**-** Nombre: **Database Admins**
<br>**-** Ubicacion y Organizacion: Default Location, Default Organization
<br>**-** Aplicar el filtro de view_lifecycle_environments, create_lifecycle_environments, destroy_lifecycle_environments, edit_lifecycle_environments.
<br>**-** Asociar el rol al usuario dbasuser 
<br>

<br>Solucion:
<br>
<br> Crear el Rol Database Admins
```
[root@satellite ~]# hammer role create --name 'Database Admins' --organization 'Default Organization' --location 'Default Location'
```

<br> Asignar los filtros view_lifecycle_environments, create_lifecycle_environments, destroy_lifecycle_environments, edit_lifecycle_environments al rol Database Admins
```
[root@satellite ~]# hammer filter create --permissions 'view_lifecycle_environments,create_lifecycle_environments,destroy_lifecycle_environments,edit_lifecycle_environments' --role 'Database Admins'
```
<br> Asociar el rol Database Admins al usuario dbauser
```
[root@satellite ~]# hammer user add-role --role 'Database Admins' --login 'dbauser'
```

<p><br><a href="sat.md">volver</a></p>
