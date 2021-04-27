---
title: "Que Es Un Api Rest"
date: 2021-03-22T20:46:57-05:00
tags: ["api","api rest","metodos http", "código de estado", "http", "json"]
---

![ https://images.pexels.com](https://images.pexels.com/photos/3861943/pexels-photo-3861943.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940, "https://images.pexels.com")

Un API o Interfaz de programación de aplicaciones, es un conjunto de definiciones y protocolos que nos permiten compartir información entre aplicaciones.  

Existen dos roles que intervienen en el concepto de **API’S**

* **Consumidos** es quien solicita la información.

* **Proveedor** que se encarga de proveer la información solicitada.

#### Ejemplo

 Consultar el nivel de tinta de nuestra impresora desde Windows, este último solicita la información del nivel de tinta a la impresora por lo tanto es el **Consumidor**.

 La impresora toma esta solicitud y retorna la información relacionada con el nivel de tinta por lo tanto tiene el rol de **Proveedor**.

 Esta interacción entre Windows y la impresora se realiza por medio de un **API**.


#### ¿QUÉ ES REST?
REST o **Trasferencia de Estado Representacional**, es un conjunto de principios de arquitectura, definida por **Roy Fielding** en el año **2000**. 

Se basa en la no existencia de estado, es decir información como por ejemplo las credenciales o **token** de seguridad deben ser enviadas cada vez que se solicite un recurso para poder ser identificados y no son almacenadas en el servidor.

#### Ejemplo de REST
Hacemos el llamado a un servicio que nos retorne el clima para un día determinado, para lo cual debemos enviar nuestras credenciales usuario y clave para obtener la información, en cada petición que realizásemos debemos enviar las credenciales, pues las mismas no quedan almacenadas en el servidor.


#### ¿QUÉ ES API REST? 
Es un conjunto de buenas prácticas utilizadas para el intercambio de información en aplicaciones utilizando el protocolo **HTTP** y **JSON** para el intercambio de información. 

Uno de los elementos mas importantes de las **API REST** son las **URI** (Identificador Único del Recurso), básicamente es una URL única que permita exponer un recurso. 

##### Ejemplo:
* http://..../tiendas

##### MÉTODOS HTTP
Para realizar operaciones sobre recursos contamos con los siguientes métodos:

 * **GET:** Se utiliza para acceder a los distintos recursos
 
 * **POST:** Se utiliza para realizar acciones de creación de nuevos recursos.

 * **PUT:** Se utiliza para modificar los recursos existentes.

 * **DELETE:** se utiliza para eliminar los recursos.

##### CÓDIGOS DE ESTADO

Además de la URI’s y los métodos disponemos de códigos de estado, que nos permiten identificar cual es el resultado de una operación realizada sobre un recurso, los más utilizados son los siguientes: 

* **200 Ok:** Respuesta estándar para peticiones correctas.

* **202 Create:** La petición a sido completada y se a creado un nuevo recurso.

* **400 Bad Request:** Petición errónea por parte del cliente.

* **401 Unauthorized:** Error relacionado con la autenticación o credenciales de seguridad.

* **404 Not Found:** Recurso no encontrado.

* **500 Internal Server Error:** Error del lado del servidor.


En el siguiente video explico en detalle lo planteado en este post.

{{< video type="youtube" id="BfYFBCClxJc" >}}