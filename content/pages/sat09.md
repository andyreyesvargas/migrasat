<h1>Gestión de Ciclo de Vida</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>

<p>
<strong>Meta:</strong>
<br>Conocer las vistas de recursos de Satellite
</p>
<p>
<strong>Objetivos:</strong>
<br>- Registrar una vista nueva dentro de un entorno customizado

</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de vistas
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Crear un nuevo entorno</strong>
<br><strong>- Crear y publicar una vista en el entorno</strong>
</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>


<h3><br><strong>Crear un nuevo entorno</strong></h3>
<p align="left"><img src="../images/sat103.png?raw=true"width="800" height="400"></p>

Se crea un nuevo entorno
<p align="left"><img src="../images/sat104.png?raw=true"width="800" height="400"></p>

Ingresamos los datos para el entorno de Desarrollo
<p align="left"><img src="../images/sat105.png?raw=true"width="800" height="400"></p>

Verificamos la creación del entorno DEV y agregamos uno nuevo anidado al DEV
<p align="left"><img src="../images/sat106.png?raw=true"width="800" height="400"></p>

Creamos el nuevo entorno de pruebas sujeto a DEV
<p align="left"><img src="../images/sat107.png?raw=true"width="800" height="400"></p>

Verificamos la creación de QA y agregamos uno nuevo
<p align="left"><img src="../images/sat108.png?raw=true"width="800" height="400"></p>

Ingresamos los datos del entorno PROD que será para sistemas operativos productivos
<p align="left"><img src="../images/sat109.png?raw=true"width="800" height="400"></p>

Validamos la creación de los entorno DEV > QA > PROD
<p align="left"><img src="../images/sat110.png?raw=true"width="800" height="400"></p>

Cuando los sitemass operativos se van registrando en la plataforma satellite, las versiones se van registrando en la sección de sistemas operativos, como buena practica crearemos un RHEL9 generico, para ello clonamos una version existente
<p align="left"><img src="../images/sat111.png?raw=true"width="800" height="400"></p>

Modificamos los datos para que el clone sea version 9 sin releases
<p align="left"><img src="../images/sat112.png?raw=true"width="800" height="400"></p>

Verificamos los sistemas operativos
<p align="left"><img src="../images/sat113.png?raw=true"width="800" height="400"></p>

<h3><br><strong>Crear una nueva vista de contenido</strong></h3>
<p align="left"><img src="../images/sat114.png?raw=true"width="800" height="400"></p>

Crear uno nuevo
<p align="left"><img src="../images/sat115.png?raw=true"width="800" height="400"></p>

Ingresar los datos para una vista asociada al entorno DEV para sistemas RHEL9
<p align="left"><img src="../images/sat116.png?raw=true"></p>

Ver los repositorios disponibles para la vista
<p align="left"><img src="../images/sat117.png?raw=true"></p>

Agregar los 3 repositorios para RHEL9 sincronizados en capítulos previos
<p align="left"><img src="../images/sat118.png?raw=true"></p>

Publicar una nueva version
<p align="left"><img src="../images/sat119.png?raw=true"></p>

Promoverlo en el ambiente DEV
<p align="left"><img src="../images/sat120.png?raw=true"></p>

Finalizar la publicación
<p align="left"><img src="../images/sat121.png?raw=true"></p>

Validar la creación de la vista de contenido
<p align="left"><img src="../images/sat122.png?raw=true"></p>

<h3><br><strong>Crear una nueva llave de activación</strong></h3>
<p align="left"><img src="../images/sat123.png?raw=true"></p>






























Para crear un nuevo entorno, nos dirigimos a la seccion Content > Lifecycle Environments  y le damos crear un nuevo entorno de ciclo de vida.
<br>
<br>

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10101R.jpg?raw=true"width="800" height="400"></p>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10102R.jpg?raw=true"width="800" height="400"></p>
En la pestaña de nuevo entorno colocar:<br>
Nombre: <strong>Build</strong><br>
Label: <strong>Build</strong><br> 
Descripción: <strong>Build Environment</strong><br>
<br>
Luego darle click al boton <strong>Save</strong><br>
<br>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10103R.jpg?raw=true"></p>
<br>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10104R.jpg?raw=true"width="800" height="400"></p>
Crear un nuevo entorno llamado Test que este a continuacion de Build<br>
Nombre: <strong>Test</strong><br>
Label: <strong>Test</strong><br> 
Prior Environment: <strong>Build</strong><br>
<br>
Luego darle click al boton <strong>Save</strong><br>
<br>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10105R.jpg?raw=true"></p>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10106R.jpg?raw=true"></p>
Crear un nuevo entorno llamado Test que este a continuacion de Build<br>
Nombre: <strong>Deploy</strong><br>
Label: <strong>Deploy</strong><br> 
Prior Environment: <strong>Test</strong><br>
<br>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10107R.jpg?raw=true"></p>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat10108R.jpg?raw=true"></p>

<br><h3><strong>Crear y publicar una vista en el entorno</strong></h3>

Ahora que tenemos un nuevo entorno, podemos crear una nueva vista en la seccion Content > Content Views 
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat900.png?raw=true">

Nombramos la vista nueva
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat901.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat902.png?raw=true">

En el vista nueva, seleccionamos el repositorio Base del canal de RHEL8 para incluirlo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat904.png?raw=true">

Ahora podemos publicar la vista
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat905.png?raw=true">

Guardamos la version 1 de nuestra vista
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat906.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat907.png?raw=true">
Cuando termine de publicar, con le damos click al boton promover
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat908.png?raw=true">

Ahora le damos check a nuestro entorno para que la vista sea promovida en ella
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat909.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat910.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat911.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat912.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat913.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat914.png?raw=true">

<br><h3><strong>Crear llaves de activación</strong></h3>
Ahora que tenemos una vista de contenido, podemos crear una llave de activación Content > Activation Keys 

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat915.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat916.png?raw=true">

Ingresar los datos del nombre de la llave de activación, seleccionar el ambiente y crear

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat917.png?raw=true">

Asegurarse que este seleccionada la versión de Red Hat Enterprise Linux 8

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat918.png?raw=true">

Seleccionar las suscripciones validas para la llave de activacion

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat919.png?raw=true">

Asegurarse que los repositorios correctos estén habilitados

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat920.png?raw=true">

## Laboratorio de la Unidad
<br>1. Cree un nuevo entorno de ciclo de vida que contengo lo siguiente: **DesarrolloX**, **CertificacionX**, **ProduccionX**. Donde **X** es reemplazado por el numero de estación de cada asistente que va del **1** al **6**. Ejemplo: Desarrollo9, Certificacion9, Produccion9.
<br>
<br>2. Cree una vista de contenido llamado BaseX, en la versión inicial solamente adicione el repositorio yum: Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 8 y publíquelo. Una vez publicado promuévalo a los ambientes **DesarrolloX, CertificacionX y ProduccionX**.
<br>
<br>3. Genere una nueva versión 2.0 de la vista de contenido Base que incluya los repositorios: **Red Hat Enterprise Linux 8 for x86_64 - AppStream RPMs 8** y **Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 RPMs**  y promuevalo a los ambientes: **DesarrolloX, CertificacionX y ProduccionX**.
<br>
<br>4. Genere una llave de activación para realizar un re-registro del clienteX de su laboratorio, utilizar los siguientes datos:
       ActivationKey Name: **AK_BASE_RHEL8_PROD_USER_X**.<br>
       En ambiente seleccionar: **ProduccionX**<br>
       Vista de Contenido: **BaseX**<br>
       Tab de suscripciones: **Asegurarse que la opción de auto-attach si este habilitada**<br>
       Tab de Juego de repositorios: **Habilitar los repositorios correspondientes**<br>
       Finalmente Registrar el cliente correspondiente utilizando la llave de activación creada: <br>
       **subscription-manager register --org="Opennova" --activationkey="AK_BASE_RHEL8_PROD_USER_X"**<br>
       verificar que dispone de los repositorios configurados en la vista de contenido. Pruebe instalar el paquete **zsh**.

Nota: Para des-registrar un cliente hacerlo de la opción Host > Content Host, seleccionar su cliente y en la parte superior derecha en la opción de selección darle delete.

En el terminal del cliente ejecutar:
```
[root@client01 ~]# subscription-manager unregister
[root@client01 ~]# subscription-manager clean
[root@client01 ~]# yum clean all
```
Luego utilizar su llave de activación nueva y validar que su cliente este registrado correctamente dentro de Host > Content Host

<br>




<p><br><a href="sat.md">volver</a></p>
