# Instalación de servicios REST/WS Wildfly

![logo](https://github.com/Regnierd/Wildfly/blob/main/img/logo.png)

## Índice

- <a href="#1">1. Requisitos previos</a>
- <a href="#2">2. Desplegar dos servicios</a>


<a name="1"></a>

### 1. Requisitos previos
Para poder realizar esta práctica necesitaremos tener instalado <b>Java, Maven y Wildfly</b> de la práctica anterior.  Añadiendo una cuenta de superusuario que no sea root.

<a name="2"></a>

### 2. Desplegar dos servicios
Antes de empezar a desplegar las aplicaciones tendremos que descargarnos unos ejemplos para Wildfly. Para ello, abriremos el siguiente enlace <a href="https://github.com/wildfly/quickstart/">Wildfly quickstart ejemplos</a> y clonamos el repositorio en nuestra máquina.

![1](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/1.png)

### 2.1 Rest
Una vez que se clone iremos al directorio de <b>helloworld-rs</b> y ejecutamos el siguiente comando: <b>mvn clean install</b>. Sirve para compilar el código del proyecto, gracias a Maven.

![2](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/2.png)

Una vez logueados en la consola de Wildfly en un navegador, procedemos a desplegar el proyecto. Para ello iremos a Deployment y agregamos un nuevo proyecto.

![3](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/3.png)

Tendremos que seleccionar en el archivo helloworld-rs.war. 

![4](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/4.png)

Una vez seleccionamos le damos a siguiente.

![5](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/5.png)

Dejamos todos los datos por defecto y le damos a Finish.

![6](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/6.png)

Y veremos como se carga con éxito.

![7](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/7.png)

A continuación tenemos que poner en una pestaña de navegador la siguiente ruta: <b>localhost:8084/helloworld-rs</b>  y veremos la siguiente imagen.

![8](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/8.png)

Si clickeamos en el apartado <b>JSON</b> vemos como se nos carga la siguiente imagen.

![9](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/9.png)

O si clickeamos en el otro apartado <b>XML</b> nos saldrá lo siguiente.

![10](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/10.png)

### 2.2 WS
Ahora probaremos con otro proyecto, pero en este caso será web-service. Hacemos lo mismo de antes usando el comando:<b> mvn clean install</b>, para la compilación.

![11](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/11.png)

Volvemos a ir a la consola de Wildfly y agregamos un nuevo proyecto. Seleccionamos el paquete <b>helloworld-ws.war</b> y le damos a abrir.

![12](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/12.png)

Dejamos todo por defecto y le damos a siguiente.

![13](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/13.png)

Volveremos a ver que se ha cargado todo correctamente y le damos a cerrar.

![14](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/14.png)

Abrimos otra ventana y ponemos de url:<b> localhost:8084/helloworld-ws</b> y veremos la siguiente imagen.

![15](https://github.com/Regnierd/Wildfly/blob/main/DespliegueRest-WS/img/15.png)