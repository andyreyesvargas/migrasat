<h1>Registrando Hosts de contenido</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento el procedimiento de registro de host de contenido en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de los recursos host de contenido en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Registrar un host de contenido de forma manual. (Demostrativo)
<br>- Desregistrar un host de contenido de forma manual. (Demostrativo)
<br>- Registrar un host de contenido usando llaves de activación. (Demostrativo)
<br>- Registrar un host de contenido a traves de bootstrap. (Demostrativo)
<br>- Registrar un host de contenido a traves de un script customizado. (Demostrativo)
<br>- Registrar un host de contenido a traves de script generado desde la web. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Registrar un host de contenido de forma manual. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a registrar un host de contenido de forma manual a traves de los comandos subscription-manager.

**NOTA:**
<br>
Si el sistema operativo cliente se encuentra registrado ejecutar los siguientes comandos.
```
[root@client01 ~]# subscription-manager unregister
[root@client01 ~]# subscription-manager clean
[root@client01 ~]# yum clean all
```
_Luego quitarlo gráficamente de satellite entrando a **Host > Content Hosts**, seleccionar el objeto y en la parte superior derecha dentro de la lista de **Select Action** buscar la opción **Delete Hosts**_

***

Iniciamos con la descarga e instalación del paquete katello-ca-consumer el cual contiene la configuración
```
# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
# yum localinstall katello-ca-consumer-latest.noarch.rpm -y
```

Ahora registramos el sistema en el environment Library
```
# subscription-manager register --org="OpenNova" --environment="Library"
```

Para validar las suscripciones disponibles ejecutamos
```
# subscription-manager list --available
```

Para registrar el sistema con alguna suscripcion usamos el siguiente comando reemplazando el PoolID con uno disponible del comando anterior
```
# subscription-manager attach --pool=<pool disponible>
```

En caso quisieramos que se asigne una suscripcion de forma automatica
```
# subscription-manager attach --auto
```

Con el sistema suscrito, debemos verificar los repositorios de software disponibles
```
# subscription-manager repos --list
```

Para efectos de este ejercicio, vamos a registrar el sistema en 3 canales de software
<br>rhel-8-for-x86_64-baseos-rpms
<br>rhel-8-for-x86_64-appstream-rpms
<br>satellite-tools-6.10-for-rhel-8-x86_64-rpms

```
# subscription-manager repos --enable=rhel-8-for-x86_64-baseos-rpms --enable=rhel-8-for-x86_64-appstream-rpms --enable=satellite-tools-6.10-for-rhel-8-x86_64-rpms
```

Podemos sincronizar estos repositorios con el comando

```
# yum repolist
```

Finalmente instalamos algunos paquetes del tipo agente para satellite, estos paquetes estan disponibles del canal satellite-tools-6.10-for-rhel-8-x86_64-rpms
```
# yum -y install katello-host-tools
# yum -y install katello-host-tools-tracer
# yum -y install katello-agent
```

De forma opcional podemos instalar algunos paquetes que usaremos en ejercicios proximos
```
# yum install -y net-tools bind-utils sos git vim bash-completion
```

Para verificar el correcto registro de nuestro cliente ejecutamos los comandos
```
# subscription-manager status
# subscription-manager list
```

Tambien podemos ingresar a la consola web del satellite, seccion HOSTS > HOSTS DE CONTENIDO y verificamos nuestro sistema nuevo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2701.png?raw=true"width="800" height="400"></p>

# Desregistrar un host de contenido de forma manual. (Demostrativo)

Podemos desregistrar el cliente satellite desde la consola web, sin embargo para que el desregistro sea completo, debe ejecutarse desde el terminal de linux y tambien desde la consola web, para ello primero nos conectamos al cliente Linux y ejecutamos los siguientes comandos

```
# subscription-manager unregister
# subscription-manager remove --all
# subscription-manager clean
# yum clean all
```

Tambien debemos eliminar el rpm que modifica la configuracion del cliente
```
# yum remove katello-ca-consumer-satellite.opennova.pe-1.0-1.noarch
```

Finalmente, retiramos el sistema de la consola web ingresando a la seccion HOSTS > HOSTS DE CONTENIDO y seleccionamos nuestro cliente con las siguientes opciones
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2702.png?raw=true"width="800" height="400"></p>

# Laboratorio 01: 
<br>- Registre su sistema cliente en la plataforma Satellite usando el metodo manual con su usuario asignado en el environment Library
<br>- Instale los paquetes <strong>net-tools bind-utils sos git vim bash-completion</strong> en su sistema cliente
<br>- Retire el sistema registrado de la plataforma Satellite

# Registrar un host de contenido a traves de una llave de activación. (Demostrativo)

A fin de registrar un host de contenido a traves de una llave de activación, debemos crear una nueva llava, podemos crearla con el nombre AK_RHEL8_test_register_X donde X es el numero de alumno.

CONTENIDO > LLAVES DE ACTIVACION
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2703.png?raw=true"width="800" height="400"></p>

CREAR LLAVE DE ACTIVACION
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2704.png?raw=true"width="800" height="400"></p>

Nombramos la llave de activacion y definimos un ambiente, para efectos del ejercicio podemos dejarlo en Library y CV default
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2705.png?raw=true"width="800" height="400"></p>
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2706.png?raw=true"width="800" height="400"></p>

En el nuevo AK registramos la suscripcion de sistemas virtualizados ilimitados
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2707.png?raw=true"width="800" height="400"></p>

Asignamos los repositorios de
<br>rhel-8-for-x86_64-baseos-rpms
<br>rhel-8-for-x86_64-appstream-rpms
<br>satellite-tools-6.10-for-rhel-8-x86_64-rpms
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2708.png?raw=true"width="800" height="400"></p>

Con la AK creada podemos registrar el host de contenido, primero descargamos e instalamos el RPM de configuracion de satellite
```
#  curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
# yum localinstall katello-ca-consumer-latest.noarch.rpm -y
```

Registramos el host de contenido mapeando nuestra AK y la organizacion disponible
```
# subscription-manager register --org="OpenNova" --activationkey="<AK creada>"
```

Por ejemplo podemos registrar el sistema usando la llave AK_RHEL8_PROD con el comando
```
# subscription-manager register --org="OpenNova" --activationkey="AK_RHEL8_PROD"
```

Validamos la disponibilidad de los repositorios
```
# yum repolist
```

En caso de no listar los 3 repositorios, intente resuscribir el sistema con
```
# subscription-manager attach --auto
```

Al igual que el metodo manual, instalamos los agentes de satellite
```
# yum -y install katello-host-tools
# yum -y install katello-host-tools-tracer
# yum -y install katello-agent
```

De forma opcional podemos instalar algunos paquetes que usaremos en ejercicios proximos
```
# yum install -y net-tools bind-utils sos git vim bash-completion
```

# Laboratorio 02: 
<br>- Registre su sistema cliente usando la llave AK_RHEL8_PROD
<br>- Asegurese que tenga registrado los repositorios de RHEL8 BaseOS, AppStream y SatelliteTools
<br>- Instale los paquetes <strong>wget python3</strong>
<br>- Des-registre el sistema cliente de la plataforma Satellite

# Creacion de Host-Groups. (Demostrativo)
Además de la topología física de Capsule Servers, Red Hat Satellite proporciona varias unidades lógicas para agrupar hosts. Los hosts que son miembros de esos grupos heredan la configuración del grupo.

Una estructura de Host-groups bien planificada puede ayudar a simplificar el mantenimiento de la configuración de lo equipos registrados en la plataforma Satellite.

Para iniciar con la creacion de un HG ingresamos a la seccion CONFIGURAR > GRUPOS DE HOSTS
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2749.png?raw=true"width="800" height="400"></p>

Creamos un nuevo Host-Group
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2750.png?raw=true"width="800" height="400"></p>

Nombramos el Host-group e ingresamos los datos del ciclo de vida correspondiente al alumno
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2751.png?raw=true"width="800" height="400"></p>

En la opcion de red, seleccionamos el dominio respectivo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2752.png?raw=true"width="800" height="400"></p>

Seleccionamos la ubicacion respectiva
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2753.png?raw=true"width="800" height="400"></p>

En el sistema operativo, seleccionamos las opciones de 64bits y sistema EL 8
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2754.png?raw=true"width="800" height="400"></p>

Validamos la organizacion
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2755.png?raw=true"width="800" height="400"></p>

Aqui seleccionamos la llave de activacion correspondiente al ciclo de vida del alumno en ambiente Produccion
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2756.png?raw=true"width="800" height="400"></p>

Validamos la creacion del Host-Group asociado a los datos del alumno en el ciclo de vida seleccionado

# Laboratorio 03: 
<br>- Cree un Host-Group ´propio con el nombre HG_RHEL8_USER_X donde X es su numero de alumno
<br>- El HG creado debera agrupar sus equipos RHEL8 en el ambiente de produccion
<br>- El HG debera incluir la llave de activacion AK_BASE_RHEL8_PROD_USER_X donde X es su numero de alumno y fue creada en ejercicio previos

# Registrar un host de contenido a traves del bootstrap. (Demostrativo)

Bootstrap es un programa desarrollado en python que facilita el registro del sistema cliente en la plataforma Satellite, este programa esta publicado por default en la pagina de Satellite en la ruta PUB
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2709.png?raw=true"width="800" height="400"></p>

Descargamos el programa en nuestro sistema cliente
```
# wget https://satellite.opennova.pe/pub/bootstrap.py
```

Si desea puede examinar el programa con los comandos vi/vim o cat
```
# vi bootstrap.py
```

Intentamos ejecutar el bootstrap usando el interprete python
```
# python3 bootstrap.py --help
```

Existen muchas opciones para registrar el sistema con los argumentos disponibles en el programa, usaremos una combinacion usando recurso creados en ejercicios anteriores
```
# python3 bootstrap.py -l <usuario> -s satellite.opennova.pe -o 'OpenNova' -L 'Lima' -g <HG creado> -a <AK creado> --skip-puppet --force
```

Por ejemplo si quisieramos registrar nuestro equipo
```
# python3 bootstrap.py -l <usuario> -s satellite.opennova.pe -o 'OpenNova' -L 'Lima' -g HG_PROD_RHEL8 -a AK_RHEL8_PROD --skip-puppet --force
```

Si examinamos la salida del programa, este ya instala los agentes necesarios para futuras funcionalidades por implementar

Podemos examinar las propiedades del HOST para verificar que este inscrito en el HG definido y su registro se realizo via AK

# Laboratorio 04: 
<br>- Verifique que tiene instalado los paquetes python3 y wget, en caso de no tenerlo use un AK e instalelos de nuevo
<br>- Descarge el programa de bootstrap en su sistema cliente
<br>- Usando el programa bootstrap, registre su cliente en la plataforma Satellite
<br>- Instale los paquetes <strong>zip unzip</strong>
<br>- Des-registre el sistema cliente de la plataforma Satellite

# Registrar un host de contenido a traves de un script customizado. (Demostrativo)
Podemos crear un script en bash que facilite el registro de los sistemas operativos, en la ruta ftp://192.168.100.203/custom_resources/script.sh o ftp://classroom.opennova.pe/custom_resources/script.sh tenemos el script base como ejemplo, el cual debemos descargar y modificar, se muestra la base del script.

```
      1 #/bin/bash
      2 clear
      3 subscription-manager unregister ; subscription-manager refresh ; yum clean all
      4 curl --insecure --output bootstrap.py http://satellite.opennova.pe/pub/bootstrap.py
      5 sleep 1
      6 clear
      7
      8 read -p "Ingrese la version de sistema operativo - 6,7 u 8 : " var01
      9 read -p "Seleccione el ambiente destino: (p) Produccion, (d) Desarrollo o (q) QA : " var02
     10
     11 case $var01 in
     12
     13   "6")
     14    if [ $var02 == "p" ]
     15    then
     16    echo "RHEL6 PROD"
     17    else
     18         if [ $var02 == "d" ]
     19         then
     20         echo "RHEL6 DESA"
     21         else
     22           if [ $var02 == "q" ]
     23           then
     24           echo "RHEL6 QA"
     25           else
     26           echo "Seleccion incorrecta"
     27           fi
     28         fi
     29    fi
     30     ;;
     31
     32   "7")
     33    if [ $var02 == "p" ]
     34    then
     35    echo "RHEL7 PROD"
     36    else
     37         if [ $var02 == "d" ]
     38         then
     39         echo "RHEL7 DESA"
     40         else
     41           if [ $var02 == "q" ]
     42           then
     43           echo "RHEL7 QA"
     44           else
     45           echo "Seleccion incorrecta"
     46           fi
     47         fi
     48    fi
     49     ;;
     50
     51   "8")
     52    if [ $var02 == "p" ]
     53    then
     54    echo "RHEL8 PROD"
     55    else
     56         if [ $var02 == "d" ]
     57         then
     58         echo "RHEL8 DESA"
     59         else
     60           if [ $var02 == "q" ]
     61           then
     62           echo "RHEL8 QA"
     63           else
     64           echo "Seleccion incorrecta"
     65           fi
     66         fi
     67    fi
     68     ;;
     69
     70   *)
     71     echo -n "Seleccion incorrecta"
     72     ;;
     73 esac
     74 echo ""
```
Las siguientes lineas estan destinadas a los sistemas operativos
<br> 16 20 24 para los equipos RHEL6
<br> 35 39 43 para los equipos RHEL7
<br> 54 58 62 para los equipos RHEL8

Reemplazamos esas lineas 54, 58 y 62 para ser modificadas por la linea de bootstrap que permita registrar el sistema en un CV y HG destinado al ambiente, en este caso usaremos el bootstrap reemplazando las lineas indicadas por la base:

```
python3 bootstrap.py -l <usuario> -p <contraseña> -s satellite.opennova.pe -o 'OpenNova' -L 'Lima' -g <HG creado> -a <AK creado> --skip-puppet --force
```

**NOTA: No olvidar instalar el paquete python3.**

modificamos los permisos del script una vez modificado
```
# chmod +x script.sh
```

Intentamos registrar el sistema client sobre RHEL8 en los 3 ambientes disponibles usando el mismo script con difenrentes selecciones.

Es una recomendacion compartir este script para ser reutilizado para el registro de diferentes sistemas, manteniendo seguro las credenciales en el, por ejemplo implementarlo con un usuario solo con permisos de registro

# Laboratorio 05: 
<br>- Descargar el script de: [ftp://classroom.opennova.pe/custom_resources/script.sh](ftp://classroom.opennova.pe/custom_resources/script.sh)
<br>- Analizar y utilizar para el registro del host, dar los persmisos chmod +x script.sh y ejecutar con ./script.sh desde la ruta de descarga.
<br>- Des-registre el sistema cliente de la plataforma Satellite.

# Registrar un host de contenido a traves de script generado desde la web. (Demostrativo)
Un metodo de registro implementado a partir de Satellite 6.10 es la generacion de un script de registro desde la web de satellite, este script simplica el proceso, sin embargo requiere tener creado CV y HG, la opcion de registro esta en HOST > REGISTART HOST
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2710.png?raw=true"width="800" height="400"></p>

Ingresamos los datos de organizacion, ubicacion, grupo de host y sistema operativo
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2711.png?raw=true"width="800" height="400"></p>

Seleccionamos el servidor satellite como capsula inteligente, la opcion de inseguro y generamos el script de registro
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2712.png?raw=true"width="800" height="400"></p>

Copiamos el script generado
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2713.png?raw=true"width="800" height="400"></p>

Pegamos el script en el client
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2714.png?raw=true"width="800" height="400"></p>

Verificamos que el script realice todos los pasos de registro de forma automatizada ademas que se registre en los recursos mapeados
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2715.png?raw=true"width="800" height="400"></p>

# Laboratorio 06: 
<br>- Usando la consola web de Satellite, genere un script de registro para su cliente RHEL8 en ambiente de desarrollo
<br>- Ejecute el registro de su cliente
<br>- Verifique que el sistema esta correctamente registrado
<br>- Des-registre el sistema de la plataforma Satellite
<br>- Usando la consola web de Satellite, genere un script de registro para su cliente RHEL8 en ambiente de produccion
<br>- Ejecute el registro de su cliente
<br>- Verifique que el sistema esta correctamente registrado
<br>- NO desregistre el sistema de la plataforma Satellite, lo usara para la siguiente seccion


<p><br><a href="sat">volver</a></p>
