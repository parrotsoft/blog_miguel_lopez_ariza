---
title: "Instalar MySQL en Ubuntu 20 Y Activar Conexión Remota"
date: 2021-05-19T14:24:58-05:00
tags: ["ubuntu","mysql","conexion remota","terminal","server","netstat","ufw","root"]
---


![https://pixabay.com](/images/mouse-379978_640.jpg "https://pixabay.com/")

En mi labor como desarrollador de Software me enfrento a situaciones en las que por algún motivo debo configurar entornos para desplegar aplicaciones y servicios del entorno de desarrollo.

Esta labor normalmente la realizo en Windows sin mayor esfuerzo, pero cuando el SO es Ubuntu la cosa cambia un poco y tengo leer documentación en varias fuentes, por tal motivo detallo cada uno de los pasos que realizo para configurar MySQL con acceso remoto en un servidor con Ubuntu 20 desplegado en DigitalOcean.

### INSTALACIÓN DE MYSQL

Con el siguiente comando conseguimos que Ubuntu actualice todos los repositorios actuales de paquete, es una operación recomendada antes de instalar un nuevo software.

```console
sudo apt-get update
```

Continuamos con la instalación del MySQL, para lo cual ejecutamos el siguiente comando:

```console
sudo apt-get install mysql-server
```
Una vez finaliza la instalación verificamos que el servicio de MySQL se este ejecutando de forma correcta con la siguiente instrucción:

```console
systemctl status mysql
```

!["systemctl status mysql"](/images/mysql_ubuntu/systemctl_status_mysql.png "systemctl status mysql")

### CONFIGURANDO MYSQL PARA PERMITIR CONEXIONES REMOTAS

En esta etapa del procesos, el primero comando a ejecutar nos permitirá cargar un asistente para  modificar configuraciones por defecto que trae MySQL:

```console
mysql_secure_installation
```

1. Pregunta:  Respuesta: **N**
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_1.png "systemctl status mysql")

2. Pregunta:  Digitamos una clave para nuestro servicio de MySQL.
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_2.png "systemctl status mysql")

3. Pregunta:  Respuesta **y**.
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_3.png "systemctl status mysql")

4. Pregunta:  Respuesta **y**.
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_4.png "systemctl status mysql")

5. Pregunta:  Respuesta **y**.
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_5.png "systemctl status mysql")

6. Pregunta:  Respuesta **y**.
!["systemctl status mysql"](/images/mysql_ubuntu/mysql_secure_installation_6.png "systemctl status mysql")

Ahora utilizando el editor de texto **nano** abriremos el archivo mysqld.cnf para realizar la modificación pertinente.

```console
 sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Una vez cargado el archivo buscamos el parámetro **bind-address** que por defecto tiene como valor **127.0.0.1** y cambiamos por **0.0.0.0**.

```console
 bind-address = 0.0.0.0
```

Luego,  presionamos la combinación de teclas **Ctrl+x** y por ultimo la tecla **Y** para confirmar el cambio sobre el archivo mysqld.cnf.
Con lo anterior permitiremos conexiones remotas a MySQL desde cualquier IP.

Continuamos ejecutando el siguiente comando que nos permitirá reiniciar el servicio de MySQL para aplicar los cambios en la configuración.

```console
 sudo systemctl restart mysql
```

Continuamos con la instalación de la herramienta **net-tools** esta nos permitirá verificar que la conexión remota a MySQL esta bien configurada. 

* Instalamos net-tools
```console
apt-get install net-tools
```
* Verificamos que las conexiones externas esten permitidas al servicio MySQL desde el puerto **3306**
```console
sudo netstat -plunt | grep mysqld
```

* Ahora crearemos con el siguiente comando un excepción en el **Firewall** de Ubuntu para el servicio MySQL.

```console
sudo ufw allow mysql
```

### CONEXIÓN REMOTA PARA EL USUARIO ROOT

```console
sudo mysql
```

```mysql
CREATE USER 'root'@'%' IDENTIFIED BY 'Mla1043605421';
```

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```

```mysql
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'Mla1043605421';
```
