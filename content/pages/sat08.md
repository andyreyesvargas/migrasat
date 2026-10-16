<h1>Gestión de Contenido</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de paquetes de software en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de paquetes de software en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Visualizar contenido de suscripciones. (Demostrativo)
<br>- Visualizar contenido de repositorios Red Hat. (Demostrativo)
<br>- Visualizar contenido de productos. (Demostrativo)
<br>- Creación de contenido de credenciales. (Demostrativo)
<br>- Creación de contenido de productos personalizado. (Demostrativo)
<br>- Modificación de llave de activación para producto personalizado. (Demostrativo)
<br>- Crear plan de sincronizacion programado. (Demostrativo)
<br>- Visualizar contenidos sincronizados. (Demostrativo)
<br>- Laboratorio: Crear repositorio personalizado con llave de contenido personalizada y plan de sincronizacion programado de canal base.
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Visualizar contenido de suscripciones. (Demostrativo)
La siguiente demostración tiene como finalidad aprender los contenidos de software en satellite.

**Content > Subscriptions**

Visualizar la pagina de **Suscripciones** y las opciones para cagar manifiesto.

<p align="left"><img src="../images/sat74.png?raw=true"width="800" height="400"></p>

En la pagina de Suscripciones examinar las suscripciones disponibles

<p align="left"><img src="../images/sat75.png?raw=true"width="800" height="400"></p>


# Visualizar contenido de repositorios Red Hat. (Demostrativo)

**Content > Red Hat Repositories**

<p align="left"><img src="../images/sat76.png?raw=true"width="800" height="400"></p>

En la pagina de **Red Hat Repositories** Visualizar las opciones de Repositorios Disponibles y Repositorios Habilitados

<p align="left"><img src="../images/sat77.png?raw=true"width="800" height="400"></p>


# Visualizar contenido de productos. (Demostrativo)

**Content > Product**

<p align="left"><img src="../images/sat78.png?raw=true"width="800" height="400"></p>

Hacer click en el producto Red Hat Enteprise Linux for x86_64 y visualizar el tab Repositorios

<p align="left"><img src="../images/sat79.png?raw=true"width="800" height="400"></p>

Hacer click en el producto Red Hat Enteprise Linux Server y visualizar el tab Repositorios

<p align="left"><img src="../images/sat80.png?raw=true"width="800" height="400"></p>

Examinar el contenido del repositorio

<p align="left"><img src="../images/sat81.png?raw=true"width="800" height="400"></p>

# Creación de contenido de credenciales. (Demostrativo)

**Content > Content Credentials**

<p align="left"><img src="../images/sat82.png?raw=true"width="800" height="400"></p>

En la pagina de **Content Credentials** hacer click en el botón **Create Content Credential**

<p align="left"><img src="../images/sat83.png?raw=true"width="800" height="400"></p>

Ingresar la información como se muestra en pantalla. En el botón examinar deberán ubicar el archivo **RPM-GPG-KEY-CUSTOM-9.txt** descargado desde el ftp://ftp.migraciones.gob.pe

<p align="left"><img src="../images/sat84.png?raw=true"width="800" height="400"></p>

Verificar que el contenido de la credencial se haya creado de manera satisfactoria.

<p align="left"><img src="../images/sat85.png?raw=true"width="800" height="400"></p>

# Creación de contenido de productos personalizado. (Demostrativo)

Para esta seccion utilizar el rpm jfrog-cli-2.124.0-1.el9.x86_64.rpm disponible en el ftp://ftp.migraciones.gob.pe y la llavee GPG importada en secciones anteriores.

Ingersar a la sección de productos
<p align="left"><img src="../images/sat86.png?raw=true"width="800" height="400"></p>

En la pagina de Productos dar click al boton **Crear Product**
<p align="left"><img src="../images/sat87.png?raw=true"width="800" height="400"></p>

Ingresar la información como se muestra en la siguiente imagen
<p align="left"><img src="../images/sat88.png?raw=true"width="800" height="400"></p>

Luego ir al tab Repositorios y darle click al botón **Nuevo repositorio**
<p align="left"><img src="../images/sat89.png?raw=true"width="800" height="400"></p>

En la pagina siguiente, en Nuevo repositorio ingresar la información de: Nombre, Etiqueta, Descripción, Tipo.
<p align="left"><img src="../images/sat90.png?raw=true"width="800" height="400"></p>
<p align="left"><img src="../images/sat91.png?raw=true"width="800" height="400"></p>

Verificar que el repositorio Java jfrog se haya creado de manera satisfactoria e ingresamos
<p align="left"><img src="../images/sat92.png?raw=true"width="800" height="400"></p>

Hacer click al repositorio a la opcion de cargar paquete, ahi se debera cargar los paquetes: jfrog-cli-2.124.0-1.el9.x86_64.rpm
<p align="left"><img src="../images/sat93.png?raw=true"width="800" height="400"></p>

Una vez seleccionados dar al boton **Cargar**
<p align="left"><img src="../images/sat94.png?raw=true"width="800" height="400"></p>

Verificar que los paquetes se hayan cargado de manera satisfactoria, en la opcion de Recuento de contenido darle click al numero 2 en la opcion de Paquetes
<p align="left"><img src="../images/sat95.png?raw=true"width="800" height="400"></p>


# Verificación del contenido customizado. (Demostrativo)

Para poder probar el repositorio personalizado podemos registrar temporalmente un sistema cliente y realizar la instalación de productos

Utilizando su propio cliente, registrelo en su propia plataforma Satelite(El siguiente ejemplo es solo para el alumno09)
```
[root@client ~]# yum install -y http://satellite.migraciones09.gob.pe/pub/katello-ca-consumer-latest.noarch.rpm
Updating Subscription Management repositories.

Dependencies resolved.
===================================================================================================
 Package                                               Arch      Version     Repository       Size
===================================================================================================
Installing:
 katello-ca-consumer-satellite.migraciones09.gob.pe    noarch    1.0-1       @commandline     10 k

Transaction Summary
===================================================================================================

Installed:
  katello-ca-consumer-satellite.migraciones09.gob.pe-1.0-1.noarch

Complete!

[root@client ~]# subscription-manager register
Registering to: satellite.migraciones09.gob.pe:443/rhsm
Username: admin
Password:
Hint: User "admin" is member of following organizations: apps, principal, Migraciones, operaciones
Organization: Migraciones
The system has been registered with ID: f36cc047-f211-4e7d-8df8-c3062edc95f7
The registered system name is: client.migraciones09.gob.pe
```

Verifique los repositorios disponibles y habilite el repositorio customizado de jfrog
```
[root@client ~]# subscription-manager repos
+----------------------------------------------------------+
    Available Repositories in /etc/yum.repos.d/redhat.repo
+----------------------------------------------------------+
Repo ID:   rhel-9-for-x86_64-appstream-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/Library/content/dist/rhe
           l9/$releasever/x86_64/appstream/os
Enabled:   1

Repo ID:   rhel-9-for-x86_64-baseos-rpms
Repo Name: Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/Library/content/dist/rhe
           l9/$releasever/x86_64/baseos/os
Enabled:   1

Repo ID:   Migraciones_Custom_jfrog
Repo Name: jfrog
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/Library/custom/Custom/jf
           rog
Enabled:   0

Repo ID:   satellite-client-6-for-rhel-9-x86_64-rpms
Repo Name: Red Hat Satellite Client 6 for RHEL 9 x86_64 (RPMs)
Repo URL:  https://satellite.migraciones09.gob.pe/pulp/content/Migraciones/Library/content/dist/lay
           ered/rhel9/x86_64/sat-client/6/os
Enabled:   0

[root@client ~]# subscription-manager repos --enable Migraciones_Custom_jfrog
Repository 'Migraciones_Custom_jfrog' is enabled for this system.
```

Por ultimo instalamos y verificamos el RPM jgrog-cli
```
[root@client ~]# yum install -y jfrog-cli

Dependencies resolved.
===================================================================================================
 Package            Architecture    Version                Repository                         Size
===================================================================================================
Installing:
 jfrog-cli          x86_64          2.124.0-1.el9          Migraciones_Custom_jfrog           23 M

Transaction Summary
===================================================================================================
Install  1 Package

Importing GPG key 0x3228467C:
 Userid     : "Fedora (epel9) <epel@fedoraproject.org>"
 Fingerprint: FF8A D134 4597 106E CE81 3B91 8A38 72BF 3228 467C
 From       : https://satellite.migraciones09.gob.pe/katello/api/v2/repositories/8/gpg_key_content
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                           1/1
  Installing       : jfrog-cli-2.124.0-1.el9.x86_64                                            1/1
  Running scriptlet: jfrog-cli-2.124.0-1.el9.x86_64                                            1/1
  Verifying        : jfrog-cli-2.124.0-1.el9.x86_64                                            1/1
Installed products updated.

Installed:
  jfrog-cli-2.124.0-1.el9.x86_64

Complete!
[root@client ~]# rpm -q jfrog-cli
jfrog-cli-2.124.0-1.el9.x86_64
```

Desuscribimos el cliente con los comandos
```
[root@client ~]# subscription-manager unregister
This system is currently not registered.
[root@client ~]# subscription-manager remove --all
0 subscriptions removed from this system.
[root@client ~]# subscription-manager clean
All local data removed
```


# Crear plan de sincronizacion programado. (Demostrativo)
**Content > Sync Plans** 
<p align="left"><img src="../images/sat96.png?raw=true"width="800" height="400"></p>

En la pagina de Planes de sincronizacion darle click al botón **Crear plan de sincronizacion**

<p align="left"><img src="../images/sat97.png?raw=true"width="800" height="400"></p>

En la pagina Crear plan de sincronizacion ingresar los datos como se muestra en la siguiente imagen y darle click al boton **Guardar**
<p align="left"><img src="../images/sat98.png?raw=true"width="800" height="400"></p>

Verificar en el tab de Información que el plan se haya creado de manera correcta
<p align="left"><img src="../images/sat99.png?raw=true"width="800" height="400"></p>

En el tab de Productos se deberá añadir el producto para la sincronizacion programada
<p align="left"><img src="../images/sat100.png?raw=true"width="800" height="400"></p>

Validar que el producto se ha ingresado de manera correcta
<p align="left"><img src="../images/sat101.png?raw=true"width="800" height="400"></p>

Si el plan se ejecuta correctamente en el tiempo, la ventana de sincronización de contenido deberia actualizarse constantemente
<p align="left"><img src="../images/sat102.png?raw=true"width="800" height="400"></p>


# Laboratorio de la Unidad: 
**NOTA: Utilizar el recursos disponibles en ftp://ftp.migraciones.gob.pe para completar el laboratorio de la unidad**

<br>**1. Crear una credencial de nombre "CustomX GPG KEY" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> La llave gpg la podrá descargar del recurso compartido.
<br>
<br>**2. Crear un Producto de nombre "Custom Product" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> El nombre del repositorio del Producto se llamara "jfrog" y podrá descargar los paquetes del recurso compartido
<br>

<br>**3. Registrar el cliente e instalar el paquete del repositorio customizado**
<br> Utilizar su cliente disponible y acorde a la demostración, instalar el paquete jfrog-cli con el repositorio customizado, no use la descarga manual de RPM e instalacion local con yum/dnf, use el repositorio customizado del producto customizado.
<br>Despues de instalar el RPM jfrog-cli, desuscriba el sistema client del satellite
<br>
<br>**4. Crear un plan de sincronizacion llamado "Custom Sync Plan" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> Asociar el producto "Red Hat Enterprise Linux for x86_64" y deberá ejecutarse todos los viernes a las 11:45 pm. ( Puede usar este valor en el cron personalizado 45 11 * * 5)

<p><br><a href="sat.md">volver</a></p>
