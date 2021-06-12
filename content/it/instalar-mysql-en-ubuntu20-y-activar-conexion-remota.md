---
title: "Instalar MySQL en Ubuntu 20 Y Activar Conexión Remota"
date: 2021-05-19T14:24:58-05:00
tags: ["ubuntu","mysql","conexion remota","terminal","server","netstat","ufw","root"]
draft: true
---


![https://pixabay.com](/images/mouse-379978_640.jpg "https://pixabay.com/")

En mi labor como desarrollador de Software me enfrento a situaciones en las que por algún motivo debo configurar entornos para desplegar aplicaciones y servicios del entorno de desarrollo, esta labor normalmente la realizo en **Windows** sin mayor esfuerzo, pero cuando el SO es **Ubuntu** la cosa cambia un poco y tengo leer documentación de varias fuentes, por tal motivo detallo cada uno de los pasos que realizo para configurar **MySQL** con acceso remoto en un servidor con **Ubuntu 20** desplegado en **DigitalOcean**.

### Instalación de MySQL

1. Actualizamos los repositorios de Ubuntu:

```console
sudo apt-get update
```

2. Instalamos **MySQL**:

```console
sudo apt-get install mysql-server
```

3. Verificamos que el servicio de MySQL este corriendo:

```console
systemctl status mysql
```

!["systemctl status mysql"](/images/mysql_ubuntu/systemctl_status_mysql.png "systemctl status mysql")

### Configurar MySQL para permitir conexiones remotas

Cargamos el asistente que nos permitirá modificar configuraciones por defecto que trae MySQL:

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

Ahora utilizando el editor de texto **nano** abriremos el archivo **mysqld.cnf** para realizar la modificación pertinente.

```console
 sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Buscamos el parámetro **bind-address** que por defecto tiene como valor **127.0.0.1** y cambiamos por **0.0.0.0**.

```vim
 bind-address = 0.0.0.0
```

Presionamos **Ctrl+x** y por ultimo la tecla **Y** para confirmar el cambio sobre el archivo **mysqld.cnf**.
>Con lo anterior permitiremos conexiones remotas a MySQL desde cualquier IP.

Reiniciamos el servicio de **MySQL** para aplicar los cambios.

```console
 sudo systemctl restart mysql
```

Continuamos con la instalación de la herramienta **net-tools** esta nos permitirá verificar que la conexión remota a MySQL esta bien configurada. 

* Instalamos net-tools
```console
apt-get install net-tools
```
* Verificamos que las conexiones externas estén permitidas al servicio MySQL desde el puerto **3306**
```console
sudo netstat -plunt | grep mysqld
```

* Ahora crearemos una excepción en el **Firewall** de Ubuntu para el servicio MySQL.

```console
sudo ufw allow mysql
```

### Conexión remota para el usuario root

```console
sudo mysql
```

```sql
CREATE USER 'root'@'%' IDENTIFIED BY 'tu_clave';
```

```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```

```sql
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'tu_clave';
```

Luego se seguir los pasos anteriores ya deberías poder acceder a tu servicio MySQL desde cualquier maquina utilizando un cliente como Navicat o HeidiSql.

Espero sea de mucha utilidad.