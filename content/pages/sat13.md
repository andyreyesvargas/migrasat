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
<br>- Ejecución de comandos remotos vía ansible playbooks. (Demostrativo)
<br>- Ejecución de comandos remotos vía ansible roles. (Demostrativo)
<br>- Laboratorio: Ejecución de tareas remotas con ansible playbooks y ansible roles
</p>
<p>
<strong>Laboratorios:</strong>
</p>
</p>

## Ejecución de comandos remotos vía ansible roles. (Demostrativo)

Para crear un rol de ansible a traves de Satellite, primero se debe ingresar a la sección
<p align="left"><img src="../images/sat196.png?raw=true">



Descargar en el servidor cliente la siguiente plantilla de ansible playbook
```
# wget ftp://192.168.100.203/ansible/playbook-workshop.yml
```
Inspeccionar y discutir el contenido de la plantilla.

Para generar una plantilla de ansible playbook en Red Hat Satellite ir a **Hosts > Job templates**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1035.png?raw=true">

Luego seleccionar la opción de **Nueva plantilla de trabajo**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1036.png?raw=true">

Dentro del Tab Plantilla ingresar:

* Plantilla De Trabajo|Nombre: **Custom SSH Banner**
* En el editor: Copiar y pegar el **contenido** del **playbook-workshop.yml**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1037.png?raw=true">

Dentro del tab Entradas:

* Agregar entrada

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1038.png?raw=true">

Dentro del tab Entradas ingresar:

* Template Input|Name: **banner_var**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1039.png?raw=true">

Dentro del tab Empleo ingresar:

* Categoría de trabajo: **Ansible Playbook**
* Provider Type: **Ansible**

y darle **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1040.png?raw=true">

Seleccionar dentro de **Host > Todo los hosts** el cliente correspondiente y darle click al **nombre**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1041.png?raw=true">

Seleccionar la opción de **Programar trabajo remoto**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1042.png?raw=true">

En la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Playbook**
* Plantilla de trabajo: **Custom SSH Banner**
* banner_var: **My custom ssh banner from Satellite!**

y dale click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1043.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1044.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1045.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/issue**

y darle **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1046.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1047.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1048.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/issue
My custom ssh banner from Satellite!
# cat /etc/ssh/sshd_config | grep Banner
Banner /etc/issue
```
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1049.png?raw=true">

## Ejecución de comandos remotos vía ansible roles. (Demostrativo)

Descargar en el servidor cliente la siguiente plantilla de ansible playbook
```
# wget ftp://192.168.100.203/ansible/ansible-role-motd.tgz
# tar -zxvf ansible-role-motd.tgz
```
Inspeccionar el contenido de los archivos y discutir.

Dentro del servidor satellite se puede generar un esqueleto de un ansible rol con el siguiente comando:
```
[root@satellite roles]# cd /etc/ansible/roles
[root@satellite roles]# ansible-galaxy init workshop-role
- Role workshop-role was created successfully
[root@satellite roles]# ls -l  workshop-role/
total 4
drwxr-xr-x. 2 root root   22 Apr 18 22:16 defaults
drwxr-xr-x. 2 root root    6 Apr 18 22:16 files
drwxr-xr-x. 2 root root   22 Apr 18 22:16 handlers
drwxr-xr-x. 2 root root   22 Apr 18 22:16 meta
-rw-r--r--. 1 root root 1328 Apr 18 22:16 README.md
drwxr-xr-x. 2 root root   22 Apr 18 22:16 tasks
drwxr-xr-x. 2 root root    6 Apr 18 22:16 templates
drwxr-xr-x. 2 root root   39 Apr 18 22:16 tests
drwxr-xr-x. 2 root root   22 Apr 18 22:16 vars
```

Para importar un rol utilizar las opciones **Configurar > Roles**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1050.png?raw=true">

En la pantalla de Ansible Roles darle click al botón **Import from satellite.opennova.pe**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1051.png?raw=true">

Seleccionar los roles que desee importar y darle al botón **Submit**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1052.png?raw=true">

Visualizar en la pagina de Ansible Roles que se muestren los roles seleccionados.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1053.png?raw=true">

Para importar o crear una variable de ansible seleccionar **Configurar > Variables**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1054.png?raw=true">

En la pagina de Ansible Variables seleccionar **New Ansible Variable**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1055.png?raw=true">

En la seccion de **Ansible Variable Details** ingresar la siguiente información:

* Clave De Busqueda|Clave: **new_var**
* Ansible Role: **motd**

En la seccion de Comportamiento predeterminado ingresar la siguiente información:
* Clave De Busqueda|Anular: **darle click a la casilla para activar.**
* Parameter Type: **cadena**
* Valor Predeterminado: **Bienvenido al Workshop Red Hat Satellite!**

y darle click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1056.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1057.png?raw=true">

Validar que en la pagina de **Ansible Variables**, se muestre la variable **new_var**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1058.png?raw=true">

En la opción **Hosts > Todo los hosts** seleccionar el nombre de la maquina cliente.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1059.png?raw=true">

Seleccionar la opción **Editar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1060.png?raw=true">

En el tab de **Ansible Roles** seleccionar el rol **motd**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1061.png?raw=true">

Seleccionar de la lista de **Programar trabajo remoto** la opción **Run Ansible roles**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1062.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1063.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1064.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/motd**

y le damos **click** al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1065.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1066.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1067.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/motd
Este es un ejemplo de /etc/motd creado durante el workshop utilizando Ansible y Satellite.

Este es un ejemplo de variable enviada a través de Satellite: Bienvenido al Workshop Red Hat Satellite!
```

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1068.png?raw=true">

Si queremos que la variable no sea aplicada globalmente podemos entrar a la seccion de **Configurar > Variables**, seleccionar la variable **new_var** y en la seccion de **Comportamiento predeterminado** des-seleccionar la opción de **Clave de Busqueda|Anular** y darle click al botón enviar.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1069.png?raw=true">

Entramos a la opción de Editar de nuestro cliente y dentro del Tab de Parámetros ingresamos:

Seccion Parámetros de Host

* new_var: cadena : Bienvenido al Workshop Red Hat Satellite! - Ejecución remota Ansible Roles!

y le damos click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1070.png?raw=true">

Seleccionamos de la lista de **Programar trabajo remoto** la opción **Run Ansible Roles**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1071.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1072.png?raw=true">

Volvemos a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **cat /etc/motd**

y le damos click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1073.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1074.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1075.png?raw=true">

Simular un logeo y validar que podamos visualizar el banner correspondiente en el cliente ejecutando:
```
# ssh root@client01
# cat /etc/motd
Este es un ejemplo de /etc/motd creado durante el workshop utilizando Ansible y Satellite.

Este es un ejemplo de variable enviada a través de Satellite: Bienvenido al Workshop Red Hat Satellite! - Ejecucion Remota Ansible Roles!
```
<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1076.png?raw=true">

### Laboratorio
1. Con el contenido de ftp://192.168.100.203/ansible/playbook-workshop.yml crear una plantilla que contenga la siguiente información:
**Pista:**
Dentro del Tab Plantilla ingresar:

* Plantilla De Trabajo|Nombre: **Custom SSH Banner User X**
* En el editor: Copiar y pegar el **contenido** del **playbook-workshop.yml**

Dentro del tab Entradas:

* Agregar entrada

Dentro del tab Entradas ingresar:

* Template Input|Name: **banner_var**

Dentro del tab Empleo ingresar:

* Categoría de trabajo: **Ansible Playbook**
* Provider Type: **Ansible**

2. Ejecutar la plantilla ansible en el cliente asignado y verificar que el banner ssh este correctamente configurado.

3. Importar el rol motd_X dentro de Red Hat Satellite, el cual deberá contener una variable con la siguiente información:
**Pista:**
En la seccion de **Ansible Variable Details** ingresar la siguiente información:

* Clave De Busqueda|Clave: **new_var**
* Ansible Role: **motd_X**

En la seccion de Comportamiento predeterminado ingresar la siguiente información:
* Clave De Busqueda|Anular: **darle click a la casilla para activar.**
* Parameter Type: **cadena**
* Valor Predeterminado: **Bienvenido al Workshop Red Hat Satellite! creado por User X**

y darle click al botón **enviar**.

4. Editar el cliente asignado y seleccionar solamente su rol motd_X y ejecutar el rol respectivo.

5. Validar vía ejecución remota y terminal que el archivo /etc/motd contenga el valor de: **Bienvenido al Workshop Red Hat Satellite! creado por User X**

<p><br><a href="sat.md">volver</a></p>
