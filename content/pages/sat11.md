<h1>Gestión de paqueteria de software</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento del proceso de instalación de software desde la plataforma de Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Instalar paquetes de software en los sistemas clienteas.(Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de actualizaciones de un sistema cliente por CLI. (Demostrativo)
<br>- Gestión de actualizaciones de un sistema cliente por GUI. (Demostrativo)
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Gestión de actualizaciones de un sistema cliente por CLI

Validamos la cantidad de erratas descubiertas en el servidor, tome nota de estos datos
```
# yum list-security
```

Si quisieramos listar solo los RHSA
```
# yum updateinfo list security
```

Podemos filtrar los RHSA por nivel de severidad
```
# yum updateinfo list updates --sec-severity=Critical
# yum updateinfo list updates --sec-severity=Important
# yum updateinfo list updates --sec-severity=Moderate
# yum updateinfo list updates --sec-severity=Low
```

Si quisieramos listar solo los RHBA
```
# yum updateinfo list bugfix
```


Seleccionamos una actualizacion del tipo bugfix para corregirlas, primero examinamos la informacion detallada de la errata
```
# yum updateinfo RHBA-2021:4543 --info
```

Tomamos la decision de aplicar la errata
```
# yum update --advisory=RHBA-2021:4543
```

Vuelva a validar la cantidad de erratas descubiertas en el servidor y compare con el reporte anterior
```
# yum updateinfo list bugfix
```

# Gestión de actualizaciones de un sistema cliente por GUI
Desde la GUI de Satellite, podemos gestionar la paqueteria de software de los sistemas registrados, para ello vamos a la seccion HOST > HOSTS DE CONTENIDO
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2736.png?raw=true"width="800" height="400"></p>

Buscamos nuestro cliente RHEL8 y vemos la seccion de actualizaciones disponibles, visto de arriba hacia abajo, se muestran las actualizaciones de seguridad, correccion, mejora y paquetes.
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2737.png?raw=true"width="800" height="400"></p>

Le damos click al nombre del equipo para ingresar a las opciones
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2738.png?raw=true"width="800" height="400"></p>

Ingresamos a la seccion de ERRATA
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2739.png?raw=true"width="800" height="400"></p>

Podemos filtrar las erratas para que solo muestre las actualizaciones de seguridad
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2740.png?raw=true"width="800" height="400"></p>

Tambien podemos filtrar por severidad, en este caso las actualizaciones criticas
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2741.png?raw=true"width="800" height="400"></p>

Tambien las del nivel moderado
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2742.png?raw=true"width="800" height="400"></p>

Si quisieras ver solo las erratas de correccion
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2743.png?raw=true"width="800" height="400"></p>

De la lista anterior de bugfixes, seleccionamos la mejora de SELinux RHBA-2021:5174, le damos click al nombre de la errata para ver los detalles
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2744.png?raw=true"width="800" height="400"></p>

Analizamos la informacion de la errata y lo que involucra la actualizacion para determinar si podemos aplicarla
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2745.png?raw=true"width="800" height="400"></p>

Si tomamos la decision de aplicar la errata, la seleccionamos en la lista y la aplicamos via remote-execution
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2746.png?raw=true"width="800" height="400"></p>

La tarea deberia ejecutarse de forma correcta
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2747.png?raw=true"width="800" height="400"></p>

Volvemos a la vista de bugfixes y validamos que la actualizacion RHBA-2021:5174 ya no este disponible
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/2748.png?raw=true"width="800" height="400"></p>

# Laboratorio 01: 
<br>- En su cliente RHEL8 instale el paquete firefox con el siguiente comando
```
# yum install firefox-68.6.0-1.el8_1.x86_64
```
<br>- Por la linea de comandos intente hacer un análisis, proponga y ejecute la actualización de ser necesaria para firefox. Una vez identificado el código puede utilizar:
```
# yum update --advisory=<Codigo_Identificado>
```


# Laboratorio 02: 
<br>- En su cliente RHEL8 instale el paquete vsftpd con el siguiente comando
```
# yum install vsftpd-3.0.3-28.el8.x86_64
```
<br>- Por la web de satellite intente hacer un análisis, proponga y ejecute la actualización de ser necesaria para vsftpd

# Laboratorio 03: 
<br>- En su cliente RHEL8 Verifique y aplique las erratas que sean solo de nivel CRITICO e IMPORTANTE

Solucion:
<br>
<br> **Verificar erratas**
```
# yum updateinfo list updates --sec-severity=Critical
# yum updateinfo list updates --sec-severity=Important
```

<br> **Aplicar erratas**
```
# yum update --sec-severity=Critical
# yum update --sec-severity=Important
```

<p><br><a href="sat">volver</a></p>
