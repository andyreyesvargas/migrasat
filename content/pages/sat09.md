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

Crear la llave nueva
<p align="left"><img src="../images/sat124.png?raw=true"></p>

Ingresar los datos de la llave referenciando al entorno DEV y al CV de RHEL9
<p align="left"><img src="../images/sat125.png?raw=true"></p>

Actualizar la llave para que se marque como sistema operativo EL 9
<p align="left"><img src="../images/sat126.png?raw=true"></p>

Agregar los repositorios de RHEL9 sincronizados en capítulos previos
<p align="left"><img src="../images/sat127.png?raw=true"></p>

<h3><br><strong>Crear una nueva grupo de hosts</strong></h3>
<p align="left"><img src="../images/sat128.png?raw=true"></p>

Crear un nuevo grupo
<p align="left"><img src="../images/sat129.png?raw=true"></p>

Ingresar los datos para que referencie a los recursos creados hasta el momento
<p align="left"><img src="../images/sat130.png?raw=true"></p>

Aunque no es relevante para el registro, podemos seleccionar la red de nuestro laboratorio
<p align="left"><img src="../images/sat131.png?raw=true"></p>

De igual manera el sistema operativo
<p align="left"><img src="../images/sat132.png?raw=true"></p>

Es importante seleccionar la llave de activación del ejercicio anterior
<p align="left"><img src="../images/sat133.png?raw=true"></p>

Verificamos la creacion del grupo de hosts
<p align="left"><img src="../images/sat134.png?raw=true"></p>


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
