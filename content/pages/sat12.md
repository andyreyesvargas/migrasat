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

### Utilizando plantillas de ejecución remota en Red Hat Satellite. (Demostrativo) 
Considerando que muchos trabajos son repetitivos y podrian ejecutarse de forma masiva, Satellite permite crear plantillas de trabajo que faciliten la ejecución remota

Vamos a crear un trabajo destinado al respaldo de toda la configuración de /etc, para ello primero ingresamos a Job Templates
<p align="left"><img src="../images/sat174.png?raw=true">

Creamos un nuevo template
<p align="left"><img src="../images/sat175.png?raw=true">

Ingresamos los datos de template como el nombre backupETC y su codigo como "tar -czvf /tmp/backup.etc.$(date +"%Y%m%d%H%M%S").tar.gz /etc/*"
<p align="left"><img src="../images/sat176.png?raw=true">

Colocamos el template en la sección de commands y lo grabamos
<p align="left"><img src="../images/sat177.png?raw=true">

Buscamos el nuevo template y podemos bloquearlo para que nadie lo edite de forma accidental
<p align="left"><img src="../images/sat178.png?raw=true">

Con el template en bash listo, regresamos al cliente
<p align="left"><img src="../images/sat160.png?raw=true">

Ejecutamos un trabajo
<p align="left"><img src="../images/sat161.png?raw=true">

Ahora en lugar de escribir un comando, buscamos el template creado
<p align="left"><img src="../images/sat179.png?raw=true">

Ejecutamos todo por default
<p align="left"><img src="../images/sat180.png?raw=true">
<p align="left"><img src="../images/sat181.png?raw=true">
<p align="left"><img src="../images/sat182.png?raw=true">
<p align="left"><img src="../images/sat183.png?raw=true">
<p align="left"><img src="../images/sat184.png?raw=true">

Tambien podemos conectarnos al cliente y verificar si el backup de etc se hiso en tmp
```
[root@client ~]# du -sh /tmp/*
4.3M    /tmp/backup.etc.20261017151213.tar.gz
```

De la misma manera, se pueden utilizar plantillas creadas en lenguaje Ansible, para ello vamos a la sección de templates
<p align="left"><img src="../images/sat185.png?raw=true">

Creamos una nueva plantilla
<p align="left"><img src="../images/sat186.png?raw=true">

Nombramos la plantilla y copiamos el codigo del programa disponible en ftp://ftp.migraciones.gob.pe/install_apache.yml
<p align="left"><img src="../images/sat187.png?raw=true">

Grabamos la plantilla cuyo objetivo es instalar el servicio apache como un Playbook de Ansible
<p align="left"><img src="../images/sat188.png?raw=true">

Tambien lo podemos bloquear para limitar las ediciones
<p align="left"><img src="../images/sat189.png?raw=true">

Ejecutamos un uevo job en el host cliente
<p align="left"><img src="../images/sat160.png?raw=true">
<p align="left"><img src="../images/sat161.png?raw=true">

Seleccionamos la plantilla de installAPACHE
<p align="left"><img src="../images/sat190.png?raw=true">

Mantenemos los valores default
<p align="left"><img src="../images/sat191.png?raw=true">
<p align="left"><img src="../images/sat192.png?raw=true">
<p align="left"><img src="../images/sat193.png?raw=true">
<p align="left"><img src="../images/sat194.png?raw=true">

Verificamos que la plantilla se ejecute correctamente
<p align="left"><img src="../images/sat195.png?raw=true">

Aunque el mensaje de satellite muestra la ejecucion en verde, podemos ir al client y verificarlo por terminal
```
[root@client ~]# rpm -q httpd
httpd-2.4.62-13.el9_8.6.x86_64
[root@client ~]# systemctl status httpd
● httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; preset: disabled)
     Active: active (running) since Mon 2026-10-19 14:58:16 -05; 47s ago
       Docs: man:httpd.service(8)
   Main PID: 4026 (httpd)
     Status: "Total requests: 0; Idle/Busy workers 100/0;Requests/sec: 0; Bytes served/sec:   0 B/>
      Tasks: 177 (limit: 22944)
     Memory: 22.4M
        CPU: 148ms
     CGroup: /system.slice/httpd.service
             ├─4026 /usr/sbin/httpd -DFOREGROUND
             ├─4027 /usr/sbin/httpd -DFOREGROUND
             ├─4028 /usr/sbin/httpd -DFOREGROUND
             ├─4029 /usr/sbin/httpd -DFOREGROUND
             └─4030 /usr/sbin/httpd -DFOREGROUND

Oct 19 14:58:16 client.migraciones09.gob.pe systemd[1]: Starting The Apache HTTP Server...
Oct 19 14:58:16 client.migraciones09.gob.pe httpd[4026]: Server configured, listening on: port 80
Oct 19 14:58:16 client.migraciones09.gob.pe systemd[1]: Started The Apache HTTP Server.
```



## Laboratorio de la Unidad
<br>1. Ejecutar las siguientes tareas remotas en el client de su infraestructura
<br>  - Usando los commands "cat /etc/redhat-release > /root/version"
<br>  - Usando Ansible "uname -r > /root/kernel"

<br>2. Crear y ejecutar la siguiente plantilla de comando: tar -czvf /tmp/backup.etc.$(date +"%Y%m%d%H%M%S").tar.gz /etc/*
<br>3. Crear y ejecutar la siguiente plantilla de Ansible: ftp://ftp.migraciones.gob.pe/install_apache.yml

**Nota: verifique todos los trabajos remotos en el cliente**

<p><br><a href="sat.md">volver</a></p>
