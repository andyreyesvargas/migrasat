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


# Modificación de llave de activación para producto personalizado. (Demostrativo)

Para poder probar el repositorio personalizado debemos hacer un ajuste a la llave de activación "rhel8" como se muestra en las imagenes. Esta llave de activacion ya cuenta con los repositorios Base y AppStream de rhel8, hay que agregarle el repositorio personalizado. Mas adelante en el entrenamiento aprendera a crear llaves de activacion.

**Content >  Activation Keys**
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat824.png?raw=true"width="800" height="400"></p>

En la pagina de Llaves de activación darle click a la llave de nombre **rhel8**
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat825.png?raw=true"width="800" height="400"></p>

Ir al tab Suscripciones e ingresar la información como se muestra en la siguiente imagen
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat826.png?raw=true"width="800" height="400"></p>

Una vez realizado esto procedemos a re-registrar nuestro cliente y registrarlo con la nueva llave de activación. Antes de comenzar se deberá borrar el registro del cliente de **Hosts > Content Hosts**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat826.png?raw=true"width="709" height="400"></p>

En el sistema operativo cliente ejecutar los siguientes comandos
```
[root@client01 ~]# subscription-manager unregister
[root@client01 ~]# subscription-manager clean
[root@client01 ~]# yum clean all
[root@client01 ~]# curl -O http://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
[root@client01 ~]# yum localinstall katello-ca-consumer-latest.noarch.rpm
[root@client01 ~]# subscription-manager register --org="OpenNova" --activationkey="rhel8"
```
NOTA: En caso que no suscriba correctamente el recurso ejecutar el siguiente comando:
```
[root@client01 ~]# subscription-manager attach --auto
[root@client01 ~]# yum repolist
```


Una vez registrado consultar los repositorios disponibles
```
[root@client01 ~]# yum repolist
Updating Subscription Management repositories.
repo id                                                      repo name
Default_Organization_Custom_Java_IBM                         Java IBM
rhel-8-for-x86_64-appstream-rpms                             Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
rhel-8-for-x86_64-baseos-rpms                                Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
satellite-tools-6.7-for-rhel-8-x86_64-rpms                   Red Hat Satellite Tools 6.7 for RHEL 8 x86_64 (RPMs)
```

Listar el paquete especifico de java ibm
```
[root@client01 ~]# yum list java-1.8.0-ibm*
Updating Subscription Management repositories.
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                                30 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.7 for RHEL 8 x86_64 (RPMs)                                                    31 kB/s | 2.1 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                   36 kB/s | 2.4 kB     00:00
Java IBM                                                                                                26 kB/s | 2.1 kB     00:00
Available Packages
java-1.8.0-ibm.x86_64                                 1:1.8.0.6.15-1.el8_2                         Default_Organization_Custom_Java_IBM
java-1.8.0-ibm-headless.x86_64                        1:1.8.0.6.15-1.el8_2                         Default_Organization_Custom_Java_IBM
```

Instalar el paquete con el siguiente comando
```
[root@client01 ~]# yum install -y java-1.8.0-ibm
```
Consultar el paquete instalado
```
[root@client01 ~]# rpm -qa | grep java-
java-1.8.0-ibm-headless-1.8.0.6.15-1.el8_2.x86_64
java-1.8.0-ibm-1.8.0.6.15-1.el8_2.x86_64
```

# Crear plan de sincronizacion programado. (Demostrativo)
**Content > Sync Plans** 
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat827.png?raw=true"width="800" height="400"></p>

En la pagina de Planes de sincronizacion darle click al botón **Crear plan de sincronizacion**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat828.png?raw=true"width="800" height="400"></p>

En la pagina Crear plan de sincronizacion ingresar los datos como se muestra en la siguiente imagen y darle click al boton **Guardar**
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat829.png?raw=true"width="800" height="400"></p>

Verificar en el tab de Información que el plan se haya creado de manera correcta
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat830.png?raw=true"width="800" height="400"></p>

En el tab de Productos se deberá añadir el producto para la sincronizacion programada
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat831.png?raw=true"width="800" height="400"></p>

Validar que el producto se ha ingresado de manera correcta
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat832.png?raw=true"width="800" height="400"></p>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat833.png?raw=true"width="800" height="400"></p>

Ir nuevamente al tab de Información y verificar que tenga en Información básica la cantidad de 1 en Productos como se muestra en la imagen
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat834.png?raw=true"width="800" height="400"></p>

En Planes de sincronizacion se deberá haber creado el plan indicado
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat835.png?raw=true"width="800" height="400"></p>

# Visualizar contenidos sincronizados. (Demostrativo)
**Content > Sync Status** 

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat836.png?raw=true"width="800" height="400"></p>

Visualizar el estado de la sincronizacion de los productos
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat837.png?raw=true"width="800" height="400"></p>

# Laboratorio de la Unidad: 
**NOTA: Utilizar el recurso ftp://classroom.opennova.pe/custom_resources/ o ftp://192.168.100.203/custom_resources/ ahi encontrara la llave GPG y los paquetes de java IBM**

<br>**1. Crear una credencial de nombre "CustomX GPG KEY" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> La llave gpg la podrá descargar del recurso compartido.
<br>
<br>**2. Crear un Producto de nombre "CustomX Java" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> El nombre del repositorio del Producto se llamara "Java IBM" y podrá descargar los paquetes del recurso compartido
<br>
<br>**3. Deberá actualializar la llave de activación AK_RHEL8_USER_X como se indica en la demostración, utilizar el procedimiento como referencia**
<br> Deberá suscribir el producto CustomX Java a la llave de activación
<br>
<br>**4. Registrar el cliente con la llave de activación AK_RHEL8_USER_X modificada como se indica en la demostración para que incluya el canal personalizado CustomX Java, utilizar el procedimiento como referencia**
<br> Borrar el cliente asignado de la pagina de Host de contenido y luego aplicar los comandos subscription-manager para des-registrar u registrar el host de contenido con la nueva llave. Adicionalemente deberá instalar el paquete java-1.8.0-ibm, este deberá poder instalarse sin errores.
<br>
<br>**5. Crear un plan de sincronizacion llamado "CustomX Sync Plan" como se indica en la demostración, utilizar el procedimiento como referencia**
<br> Asociar el producto "CustomX Java" y deberá ejecutarse todos los viernes a las 11:45 pm. ( Puede usar este valor en el cron personalizado 45 11 * * 5)

<p><br><a href="sat">volver</a></p>
