# Instalación de Wildfly en linux

![logo](https://github.com/Regnierd/Wildfly/blob/main/img/logo.png)

## Índice

- <a href="#1">1. Requisitos previos</a>
- <a href="#2">2. Instalación de Wildfly</a>
- <a href="#3">3. Acceso</a>
- <a href="#4">4. Añadir usuarios a Wildfly</a>
- <a href="#5">5. Gestionar la consola de forma remota</a>

<a name="1"></a>

### 1. Requisitos previos
Para empezar tenemos que tener instalado previamente Java y Maven para futuras prácticas.
Una vez que tengamos todo esto, empezaremos por actualizar los repositorios de Ubuntu.

![1](https://github.com/Regnierd/Wildfly/blob/main/img/1.png)

<a name="2"></a>

### 2. Instalación de Wildfly
Una vez realizada la instalación de los repositorios podemos empezar a instalar Wildfly como servicio para despliegue de aplicaciones. Para ello, usaremos el comando wget para descargar Wildfly desde el repositorio de Wildfly. El comando quedaría tal que así: <b>wget https://github.com/wildfly/wildfly/releases/download/25.0.0.Final/wildfly-25.0.0.Final.tar.gz</b>

![2](https://github.com/Regnierd/Wildfly/blob/main/img/2.png)

Cuando acabe de instalar Wildfly, pasaremos a crear un usuario y grupo wildfly. Para ellos usaremos los dos comandos siguientes:
- sudo groupadd -r wildfly
- sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly

![3](https://github.com/Regnierd/Wildfly/blob/main/img/3.png)

Descomprimimos el paquete que descargamos anteriormente con el comando: <b>tar -xvzf wildfly-25.0.0.Final.tar.gz</b>

![4](https://github.com/Regnierd/Wildfly/blob/main/img/4.png)

Cuando acabe de descomprimir el paquete lo movemos a la siguiente ruta: <b>/opt/wildfly</b>. Al cual le daremos los permisos de acceso al usuario wildfly con el siguiente comando: <b>sudo chown -R wildfly:wildfly /opt/wildfly/.</b>

![5](https://github.com/Regnierd/Wildfly/blob/main/img/5.png)

Ahora procederemos a iniciar el servicio de wildfly. Para ello creamos el directorio: <b>/etc/wildfly</b>. Luego copiamos el fichero wildfly.conf en la ruta creada anteriormente.

![6](https://github.com/Regnierd/Wildfly/blob/main/img/6.png)

Podemos verificar que el modo de arranque por defecto es standalone en el fichero que acabamos de copiar.

![7]https://github.com/Regnierd/Wildfly/blob/main/img/7.png()

Seguimos copiando los siguientes ficheros para seguir configurando el arranque:
- launch.sh
- wildfly.service 

![8](https://github.com/Regnierd/Wildfly/blob/main/img/8.png)

Iniciamos el servicio wildfly con el comando <b>sudo systemctl start wildfly</b>. Verificamos que el servicio está activo con el comando <b>sudo systemctl status wildfly</b>. Y por último, habilitamos el servicio para que se encienda automáticamente cada vez que encendamos el servidor con el comando: <b>sudo systemctl enable wildfly</b>.

![9](https://github.com/Regnierd/Wildfly/blob/main/img/9.png)

<a name="3"></a>

### 3. Acceso
Para poder acceder sin problema a Wildfly tendremos que cambiar el puerto para poder acceder. Para ello iremos a la siguiente ruta y modificamos el siguiente fichero:
<b>/opt/wildfly/standalone/configuration/standalone.xml</b>,  buscamos la siguiente línea marcada por la flecha y el puerto <b>8080</b> lo cambiamos a <b>8084</b>.

![10](https://github.com/Regnierd/Wildfly/blob/main/img/10.PNG)

![11](https://github.com/Regnierd/Wildfly/blob/main/img/11.PNG)

Después de hacer el cambio tenemos que permitir el tráfico por ese puerto, usaremos el siguiente comando: <b>sudo ufw allow 8084/tcp</b>.

![12](https://github.com/Regnierd/Wildfly/blob/main/img/13.PNG)

Una vez hecho todo esto, abrimos un navegador y ponemos la siguiente ruta: <b>localhost:8084</b>, y veremos la siguiente pantalla.

![13](https://github.com/Regnierd/Wildfly/blob/main/img/14.PNG)

<a name="4"></a>

### 4. Añadir usuarios a Wildfly
Para crear un usuario administrador en nuestro Wildfly tendremos que ejecutar el siguiente comando: <b>sudo /opt/wildfly/bin/add-user.sh</b>, el cual ejecutará un script para crear el usuario. Ponemos el nombre del usuario y su contraseña y luego pondremos <b>yes</b> a las dos opciones que nos da a continuación.

![14](https://github.com/Regnierd/Wildfly/blob/main/img/15.PNG)

<a name="5"></a>

### 5. Gestionar la consola de forma remota
Verificamos en los dos siguientes archivos estos datos que se muestran en la siguiente imagen.

![15](https://github.com/Regnierd/Wildfly/blob/main/img/16.PNG)

Para finalizar tendremos que modificar el fichero wildfly.service en la línea: 

    ExecStart=/opt/wildfly/bin/launch.sh $WILDFLY_MODE $WILDFLY_CONFIG $WILDFLY_BIND  

y  agregar al final esto:

    $WILDFLY_CONSOLE_BIND

Después reseteamos el servicio daemon-reload y el wildfly.

![16](https://github.com/Regnierd/Wildfly/blob/main/img/17.PNG)

Volvemos a un navegador y probamos que funciona entrando a la consola como administrador. Para ellos tendremos que poner la siguiente ruta: localhost:8084/console, agregaremos el usuario y contraseña y nos tendría que salir la siguiente pantalla.

![17](https://github.com/Regnierd/Wildfly/blob/main/img/18.PNG)

