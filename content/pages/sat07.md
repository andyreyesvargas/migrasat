<h1>Gestión de manifiestos y repositorios</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de manifiestos y repositorios en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Importar manifiestos a Red Hat Satellite y activar canales de software de Red Hat
</p>
<p>
<strong>Secciones:</strong>
<br>- Que es es un manifiesto de Red Hat Satellite?. (Teoría)
<br>- Generando un manifiesto de Red Hat Satellite. (Demostrativo)
<br>- Asignando manifiestos a organizaciones. (Demostrativo)
<br>- Activando repositorios oficiales de Red Hat. (Demostrativo)
<br>- Sincronizando repositorios oficiales de Red Hat. (Demostrativo)

</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Que es es un manifiesto de Red Hat Satellite?. (Teoría)
El manifiesto es un archivo comprimido que contiene una lista de suscripciones, la suscripción define los repositorios de productos y contenidos. En Red Hat Satellite Server, tenemos que importar el archivo de manifiesto y luego los repositorios de Red Hat estarán visibles en el panel de satélite.

# Generando un manifiesto de Red Hat Satellite. (Demostrativo)
El instructor demostrara como crear un manifiesto de pruebas desde la pagina de Red Hat
<p align="left"><img src="../images/sat56.png?raw=true"width="800" height="400"></p>

# Asignando manifiestos a organizaciones. (Demostrativo)
Antes de iniciar el proceso de asignar manifiestos a las organizaciones, el instructor compartirá en la ruta <strong>ftp://classroom.opennova.pe o ftp://192.168.100.203</strong> archivos de manifiestos para el curso
<p align="left"><img src="../images/sat57.png?raw=true"width="800" height="400"></p>

Se compartirá algunos manifiestos de prueba en la ruta manifiestos
<p align="left"><img src="../images/sat58.png?raw=true"width="800" height="400"></p>

Para iniciar el proceso de importación, primero debemos estar seguros de estar en la organización objetivo
<p align="left"><img src="../images/sat59.png?raw=true"width="800" height="400"></p>

Ingresamos a la sección de CONTENIDO > SUSCRIPCIONES
<p align="left"><img src="../images/sat60.png?raw=true"width="800" height="400"></p>

Procedemos a importar un manifiesto
<p align="left"><img src="../images/sat61.png?raw=true"width="800" height="400"></p>

Seleccionamos la opción de importar archivo y seleccionamos el archivo de manifiesto
<p align="left"><img src="../images/sat62.png?raw=true"width="800" height="400"></p>

El sistema proceder a importar el manifiesto
<p align="left"><img src="../images/sat63.png?raw=true"width="800" height="400"></p>

Se activaran las suscripciones disponibles en el manifiesto
<p align="left"><img src="../images/sat64.png?raw=true"width="800" height="400"></p>

# Activando repositorios oficiales de Red Hat. (Demostrativo)
Para activar repositorios disponibles en el manifiesto, vamos a la sección CONTENIDO > REPOSITORIOS DE REDHAT
<p align="left"><img src="../images/sat65.png?raw=true"width="800" height="400"></p>

Es recomendable activar la opción de REPOSITORIOS RECOMENDADOS para mostrar los repositorios mas comunes de las suscripciones
<p align="left"><img src="../images/sat66.png?raw=true"width="800" height="400"></p>

Ahora vamos a activar los repositorios mas importantes para los sistemas RHEL 9, empesando por el BaseOs
<p align="left"><img src="../images/sat67.png?raw=true"width="800" height="400"></p>

Luego Activamos el AppStream
<p align="left"><img src="../images/sat68.png?raw=true"width="800" height="400"></p>

Por ultimo el Cliente para RHEL9
<p align="left"><img src="../images/sat69.png?raw=true"width="800" height="400"></p>


# Sincronizando repositorios oficiales de Red Hat. (Demostrativo)
Para sincronizar por primera vez los repositorios activados en secciones previas, ingresamos a la sección CONTENIDO > ESTATUS DE SINCRONIZACION
<p align="left"><img src="../images/sat70.png?raw=true"width="800" height="400"></p>

En esta sección vemos todos los repositorios activados pero que nunca se han sincronizado, podemos seleccionar repositorios específicos y proceder a sincronizarlos
<p align="left"><img src="../images/sat71.png?raw=true"width="800" height="400"></p>

Esta sincronización puede demorar minutos u horas dependiendo del tamaño del repositorio, por ejemplo los repositorios de SatTools e Insigths demorara solo unos segundos, pero los de sistema operativo podrían demorar mucho mas, el objetivo es tener los repositorios siempre sincronizados como se ve en la siguiente pantalla
<p align="left"><img src="../images/sat72.png?raw=true"width="800" height="400"></p>

Como recomendación final, cuando los recursos de computo son limitados, se recomienda sincronizar un repositorio a la vez

# Asignando manifiestos a organizaciones por CLI. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear la organizaciones de operaciones
```
[root@satellite ~]# hammer organization create  --name Operaciones --label operaciones --description 'Servidores de operaciones' --location Lima
Organization created.
```
Obtener el manifiesto desde el servidor ftp
```
[root@satellite ~]# wget ftp://ftp.migraciones.gob.pe/manifiestos/manifest_MIGRA_operaciones_20261013T184234Z.zip

manifest_MIGRA_operacion 100%[=================================>]   1.28M  --.-KB/s    in 0.01s

2026-10-13 14:17:53 (99.2 MB/s) - ‘manifest_MIGRA_operaciones_20261013T184234Z.zip’ saved [1339787]
```
Importar el manifiesto descargado a la organizaciones Operaciones
```
[root@satellite ~]# hammer subscription upload --file manifest_MIGRA_operaciones_20261013T184234Z.zip --organization "Operaciones"
warning: Overriding "Content-Type" header "multipart/form-data" with "multipart/form-data; boundary=----RubyFormBoundaryz1TO09tyRfrbCNAh" due to payload
[..........................................................................................] [100%]
```
Verificar las suscripciones de la organización operaciones
```
---|----------------------------------|------------------------------------------|----------|----------|---------|---------|---------------------|---------------------|----------|----------|-------------------
ID | UUID                             | NAME                                     | TYPE     | CONTRACT | ACCOUNT | SUPPORT | START DATE          | END DATE            | QUANTITY | CONSUMED | PRODUCT HOST COUNT
---|----------------------------------|------------------------------------------|----------|----------|---------|---------|---------------------|---------------------|----------|----------|-------------------
2  | 4028ed8aa13688d401a136b4eca65719 | Red Hat Partner Subscription (500 Nodes) | Physical |          | 5257369 | None    | 2026/05/30 04:00:00 | 2027/05/30 03:59:59 | 5        | 0        | 0      
---|----------------------------------|------------------------------------------|----------|----------|---------|---------|---------------------|---------------------|----------|----------|-------------------
```
Importar el manifiesto descargado a la organizaciones Operaciones
```
[root@satellite ~]# hammer repository-set enable --organization "Operaciones" --product "Red Hat Enterprise Linux for x86_64" --name "Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)" --releasever "9"
Repository enabled.
[root@satellite ~]# hammer repository-set enable --organization "Operaciones" --product "Red Hat Enterprise Linux for x86_64" --name "Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)" --releasever "9"
Repository enabled.
[root@satellite ~]# hammer repository-set enable --organization "Operaciones" --product "Red Hat Enterprise Linux for x86_64" --name "Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)"
Repository enabled.
```
Para facilitar la sincronización, listamos los repositorios de la organización Operaciones
```
[root@satellite ~]# hammer repository list --organization Operaciones
---|----------------------------------------------------------|-------------------------------------|--------------|-------------------------------------------|-------------------------------------------------------------------------
ID | NAME                                                     | PRODUCT                             | CONTENT TYPE | CONTENT LABEL                             | URL                                  
---|----------------------------------------------------------|-------------------------------------|--------------|-------------------------------------------|-------------------------------------------------------------------------
5  | Red Hat Enterprise Linux 9 for x86_64 - AppStream RPMs 9 | Red Hat Enterprise Linux for x86_64 | yum          | rhel-9-for-x86_64-appstream-rpms          | https://cdn.redhat.com/content/dist/rhel9/9/x86_64/appstream/os
4  | Red Hat Enterprise Linux 9 for x86_64 - BaseOS RPMs 9    | Red Hat Enterprise Linux for x86_64 | yum          | rhel-9-for-x86_64-baseos-rpms             | https://cdn.redhat.com/content/dist/rhel9/9/x86_64/baseos/os
6  | Red Hat Satellite Client 6 for RHEL 9 x86_64 RPMs        | Red Hat Enterprise Linux for x86_64 | yum          | satellite-client-6-for-rhel-9-x86_64-rpms | https://cdn.redhat.com/content/dist/layered/rhel9/x86_64/sat-client/6/os
---|----------------------------------------------------------|-------------------------------------|--------------|-------------------------------------------|-------------------------------------------------------------------------
```












# Laboratorio
<br>- Con lo aprendido en esta lección, importe los manifiestos disponibles para las organizaciones Aplicaciones y Cajeros
<br>- Active los repositorios básicos de RHEL8 para la organización Aplicaciones
<br>- Sincronice los repositorios de la organización Aplicaciones
<br>- Active los repositorios básicos de RHEL7 para la organización Cajeros
<br>- Sincronice los repositorios de la organización Cajeros

**NOTA:**
Puede descargar los manifiestos de aquí:  
**wget** ftp://classroom.opennova.pe/manifiestos/manifest_aplicaciones_20230117T202214Z.zip  
**wget** ftp://classroom.opennova.pe/manifiestos/manifest_cajeros_20230117T202226Z.zip

<p><br><a href="sat">volver</a></p>
