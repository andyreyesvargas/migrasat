<h1>Gestión de ejecución remota vía Red Hat Satellite</h1>
<p align="left"><img src="../images/sat.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de ejecución remota vía Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y administración de opciones de ejecución remota en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Pre-requisitos para utilizar ejecución remota en Red Hat Satellite. (Demostrativo)
<br>- Ejecución de comandos remotos vía comandos SSH. (Demostrativo)
<br>- Ejecución de comandos remotos vía comandos Ansible . (Demostrativo)
<br>- Ejecución de comandos remotos utilizando bash shell scripting. (Demostrativo)
<br>- Laboratorio: Crear repositorio personalizado con llave de contenido personalizada y plan de sincronizacion programado de canal base.
</p>
<p>
<strong>Laboratorios:</strong>
</p>
</p>

### Pre-requisitos para utilizar ejecución remota en Red Hat Satellite. (Demostrativo) 
Para poder utilizar el procedimiento de ejecución remota el sistema operativo cliente debe estar registrado en la plataforma satellite, como se muestra en la pantalla
<p align="left"><img src="../images/sat160.png?raw=true">

Aunque el procedimiento de registro via script de satellite completa los requisitos, podemos verificar la conexión remota desde el servidor satellite al client con un comando ssh usando la llave de autenticación autogenerada con un comando remoto como hostname
```
[root@satellite ~]# ssh -i /usr/share/foreman-proxy/.ssh/id_rsa_foreman_proxy root@client.migraciones09.gob.pe "hostname"
client.migraciones09.gob.pe
```

### Ejecutar comandos remotos via Red Hat Satellite. (Demostrativo) 
Para ejecutar comandos simples que ingresemos por el terminal, ingresamos al cliente que deseamos se ejecute el comando
<p align="left"><img src="../images/sat160.png?raw=true">

Seleccionamos la opción de programar un trabajo
<p align="left"><img src="../images/sat161.png?raw=true">

Usamos la función command para ejecutarlo como un comando regular en el terminal
<p align="left"><img src="../images/sat162.png?raw=true">

Ingresamos el comando "cat /etc/redhat-release > /root/version" para obtener la versión del sistema operativo en un archivo de texto
<p align="left"><img src="../images/sat163.png?raw=true">

Aunque el sistema permite escoger otro usuario y credenciales para ejecutar el comando remoto, lo dejamos por default para usar la llave ssh validada al inicio del capitulo
<p align="left"><img src="../images/sat164.png?raw=true">

Mantenemos la ejecución en el cliente seleccionado
<p align="left"><img src="../images/sat165.png?raw=true">

Enviamos la tarea remota
<p align="left"><img src="../images/sat166.png?raw=true">

El sistema confirmara la correcta ejecución del job
<p align="left"><img src="../images/sat167.png?raw=true">

Tambien lo podemos verificar en el cliente
```
[root@client ~]# cat /root/version
Red Hat Enterprise Linux release 9.4 (Plow)
```

La ejecución de comandos tambien se puede hacer usando el motor de ansible en lugar del terminal tradicional, para ello seleccionamos el client
<p align="left"><img src="../images/sat160.png?raw=true">

Programamos un nuevo trabajo
<p align="left"><img src="../images/sat161.png?raw=true">

Cambiamos el motor a ansible con un comando ansible
<p align="left"><img src="../images/sat168.png?raw=true">

Ejecutamos el comando para obtenet la version de kernel "uname -r > /root/kernel" en el cliente remoto
<p align="left"><img src="../images/sat169.png?raw=true">

Mantenemos las opciones default
<p align="left"><img src="../images/sat170.png?raw=true">
<p align="left"><img src="../images/sat171.png?raw=true">
<p align="left"><img src="../images/sat172.png?raw=true">

El sistema nos indicara que el comando por ansible se ejecuto correctamente
<p align="left"><img src="../images/sat173.png?raw=true">

Tambien podemos verificarlo en el mismo cliente
```
[root@client ~]# cat /root/kernel
5.14.0-427.13.1.el9_4.x86_64
```















debemos haber creado un Host Group el cual nos permita utilizar tanto el Lifecycle, Content View, Activation Key, respectivos para poder hacer el registro vía script web por la opción de Host > Register Host.

Es recomendable utilizar el procedimiento de Registro de cliente utilizando el script web autogenerado por la opción Host > Register Host, ya que este a su vez internamente copia las llaves ssh del servidor satellite hacia los clientes, asi mismo realiza el procedimiento de registro en el portal de Insight y habilita el cliente insight-client.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1000.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1001.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1002.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1003.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1004.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1005.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1006.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1007.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1008.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1009.png?raw=true">

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1010.png?raw=true">

**NOTA: En el caso de utilizar otro procedimiento de registro de clientes considerar copiar las llaves ssh del servidor satellite hacia los clientes como indica la siguiente linea.**
```
[root@satellite ~]# ssh-copy-id -i ~foreman-proxy/.ssh/id_rsa_foreman_proxy.pub root@client01
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/usr/share/foreman-proxy/.ssh/id_rsa_foreman_proxy.pub"
The authenticity of host 'client01 (192.168.0.191)' can't be established.
ECDSA key fingerprint is SHA256:ofx/QmfXcWBaH9a9/7FxYP9ga7eerw0DzTLFso+IR9A.
ECDSA key fingerprint is MD5:17:47:6d:4f:39:ae:f9:30:10:76:6f:86:3c:1d:e3:1d.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
My custom ssh banner from Satellite!
root@client01's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@client01'"
and check to make sure that only the key(s) you wanted were added.
```

### Ejecución de comandos remotos vía comandos SSH. (Demostrativo)

Para ir a las opciones de ejecución remota podemos utilizar la opción de **Hosts > Todos los hosts**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1011.png?raw=true">

Luego seleccionar el cliente respectivo y darle click sobre el **Nombre**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1012.png?raw=true">

Luego seleccionar la opción de **Programar trabajo remoto**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1013.png?raw=true">

Dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Run Command - SSH Default**
* command: **df -h**

Darle click a botón **enviar**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1014.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1015.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1016.png?raw=true">

Observar la salida correcta de la tarea ejecutada remotamente.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1017.png?raw=true">

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Packages**
* Plantilla de trabajo: **Package Action - SSH Default**
* action: **install**
* package: **zsh**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1017-1.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1017-2.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1017-3.png?raw=true">

### Ejecución de comandos remotos vía comandos Ansible. (Demostrativo)

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **lsblk -f**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1018.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1019.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1020.png?raw=true">

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Packages**
* Plantilla de trabajo: **Package Action - Ansible Default**
* state: **present**
* name: **net-tools, bind-utils, sos, tree, vim**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1021.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1022.png?raw=true">

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **rpm -qa | grep -e net-tools -e bind-utils -e sos -e tree -e vim**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1023.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1024.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1025.png?raw=true">

### Ejecución de comandos remotos utilizando bash shell scripting. (Demostrativo)

Ir a las opciones de **job templates** utilizar la opción de **Hosts > Job templates**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1026.png?raw=true">

Dentro de la pagina **Plantillas de trabajo** seleccionar **Nueva plantilla de trabajo**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1027.png?raw=true">

En el tab **Plantilla** colocar la siguiente información:

* Plantilla de trabajo|Nombre: **Backup etc directory**

Descargar el siguiente script [ftp://192.168.100.203/bash/backup.sh](ftp://192.168.100.203/bash/backup.sh) a su estación cliente e inspeccionar.
```
# wget ftp://192.168.100.203/bash/backup.sh
```

* Dentro del **editor** colocar el contenido del **script backup.sh**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1028.png?raw=true">

En el tab **Empleo** seleccionar:

* Categoría de trabajo: Commands
* Provider Type: SSH

y darle click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1029.png?raw=true">

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Backup etc directory**

y darle click al botón **enviar**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1030.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1031.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1032.png?raw=true">

Clonar la plantilla de trabajo **Backup etc directory**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1033.png?raw=true">

En la opción de Plantilla de Trabajo| Nombre indicar Backup etc directory User 1 luego darle click al botón enviar, con esto ya tenemos una copia de una plantilla de trabajo. 

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1034.png?raw=true">

Verificamos que se haya creado correctamente el **clon**.

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1034-1.png?raw=true">

Volvemos nuevamente a la opción de Programación de tareas remotas dentro de la siguiente casilla seleccionaremos:

* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Backup etc directory User 1**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1034-2.png?raw=true">

Observar que la tarea haya finalizado de forma correcta con **100% Éxito**

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1034-3.png?raw=true">

En la parte inferior sobre el nombre del cliente darle **click** al nombre en **host** para verlos detalles

<p align="left"><img src="https://github.com/workshopopennova/tecnologiasredhat/blob/master/images/sat/sat1034-4.png?raw=true">

## Laboratorio de la Unidad
<br>1. Ejecutar una tarea remota utilizando la opción de comandos ssh que realice el backup del directorio /etc y lo envié al directorio /tmp, el formato del backup será etc_$(date +%d%m%Y%H%M%S).tar.xz.

Pista:
* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Run Command - SSH Default**
* command: **tar -cJvf /tmp/etc_$(date +%d%m%Y%H%M%S).tar.xz /etc**

<br>2. Validar utilizando los comandos de ejecución remota por ssh que el directorio /tmp contenga el backup generado en el punto 1.

Pista:
* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Run Command - SSH Default**
* command: **ls -l /tmp**

<br>3. Utilizando comandos de ejecución remota ssh descomprimir el backup generado en el punto 1 dentro de /var/tmp.

Pista:
* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Run Command - SSH Default**
* command: **tar -xJvf /tmp/etc_15042022144059.tar.xz -C /var/tmp**  << cambiar por el nombre de su backup

**NOTA: En el punto 2 podrá visualizar exactamente cual es el nombre de su archivo de backup tomando su actual, ese valor reemplazarlo por el indicado en la pista. Adicionalmente utilizar el comando ls -lR /var/tmp/etc/ para validar que se haya desempaquetado el backup de manera correcta, utilizar para la validación comando de ejecución remota vía Red Hat Satellite**

<br>4. Utilizando comandos de ejecución remota ansible instalar los siguientes paquetes de software: net-tools, bind-utils, sos, tree, vim, tmux, lsof.

Pista
* Categoría de trabajo: **Ansible Packages**
* Plantilla de trabajo: **Package Action - Ansible Default**
* state: **present**
* name: **net-tools, bind-utils, sos, tree, vim, tmux, lsof**

<br>5. Utilizando comandos de ejecución remota ansible valide que los paquetes instalados en el punto 4 se encuentran instalados correctamente.

Pista
* Categoría de trabajo: **Ansible Commands**
* Plantilla de trabajo: **Run Command - Ansible Default**
* command: **rpm -qa | grep -e net-tools -e bind-utils -e sos -e tree -e vim -e tmux -e lsof**

<br>6. Utilizando el contenido del script ubicado en ftp://192.168.100.203/bash/backup.sh crear una plantilla de trabajo que tenga la siguiente información:

Pista:
Tab Plantilla
* Nombre de la plantilla: **Backup etc directory User X**
* Contenido de la plantilla: Información ubicada en el script **backup.sh**

Tab Empleo
* Categoría de trabajo: Commands
* Provider Type: SSH

<br>7. Ejecutar la plantilla creado en el punto 6 y validar que haya generado el backup correspondiente.
Pista:
* Categoría de trabajo: **Commands**
* Plantilla de trabajo: **Backup etc directory User X**

**NOTA: Para validar que el script se genero de manera correcta puede ejecutar una tarea remota de tipo comando SSH o comando ansible que contenga el comando: ls -l /backups**

<br>

<p><br><a href="sat.md">volver</a></p>
