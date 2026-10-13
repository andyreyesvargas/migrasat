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
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2716a.png?raw=true"width="800" height="400"></p>

Se compartirá algunos manifiestos de prueba en la ruta manifiestos
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2716b.png?raw=true"width="800" height="400"></p>

Para iniciar el proceso de importación, primero debemos estar seguros de estar en la organización objetivo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2717.png?raw=true"width="800" height="400"></p>

Ingresamos a la sección de CONTENIDO > SUSCRIPCIONES
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2718.png?raw=true"width="800" height="400"></p>

Procedemos a importar un manifiesto
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2719.png?raw=true"width="800" height="400"></p>

Seleccionamos la opción de importar archivo y seleccionamos el archivo de manifiesto
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2720.png?raw=true"width="800" height="400"></p>

El sistema proceder a importar el manifiesto
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2721.png?raw=true"width="800" height="400"></p>

Se activaran las suscripciones disponibles en el manifiesto
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2722.png?raw=true"width="800" height="400"></p>

# Activando repositorios oficiales de Red Hat. (Demostrativo)
Para activar repositorios disponibles en el manifiesto, vamos a la sección CONTENIDO > REPOSITORIOS DE REDHAT
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2723.png?raw=true"width="800" height="400"></p>

Es recomendable activar la opción de REPOSITORIOS RECOMENDADOS para mostrar los repositorios mas comunes de las suscripciones
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2724.png?raw=true"width="800" height="400"></p>

Ahora vamos a activar los repositorios mas importantes para los sistemas RHEL 8, empesando por el BaseOs
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2725.png?raw=true"width="800" height="400"></p>

Luego Activamos el AppStream
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2726.png?raw=true"width="800" height="400"></p>

Por ultimo el SatTools para RHEL8
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2727.png?raw=true"width="800" height="400"></p>

De igual manera podemos activar los repositorios de RHEL7 empesando por el sistema operativo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2728.png?raw=true"width="800" height="400"></p>

También activamos el SatTools para RHEL7
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2729.png?raw=true"width="800" height="400"></p>

En el caso de RHEL7, es necesario activar el repositorio de Insights, este repositorio no esta disponible en los recomendados, por ello lo desactivamos y aplicamos un filtro en la búsqueda para encontrarlo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2730.png?raw=true"width="800" height="400"></p>

Activamos el repositorio de Insighys para RHEL7
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2731.png?raw=true"width="800" height="400"></p>

# Sincronizando repositorios oficiales de Red Hat. (Demostrativo)
Para sincronizar por primera vez los repositorios activados en secciones previas, ingresamos a la sección CONTENIDO > ESTATUS DE SINCRONIZACION
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2732.png?raw=true"width="800" height="400"></p>

En esta sección vemos todos los repositorios activados pero que nunca se han sincronizado, podemos seleccionar repositorios específicos y proceder a sincronizarlos
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2733.png?raw=true"width="800" height="400"></p>

Esta sincronización puede demorar minutos u horas dependiendo del tamaño del repositorio, por ejemplo los repositorios de SatTools e Insigths demorara solo unos segundos, pero los de sistema operativo podrían demorar mucho mas, el objetivo es tener los repositorios siempre sincronizados como se ve en la siguiente pantalla
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2735.png?raw=true"width="800" height="400"></p>

Como recomendación final, cuando los recursos de computo son limitados, se recomienda sincronizar un repositorio a la vez

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
