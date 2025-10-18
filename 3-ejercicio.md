## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es */var/lib/mysql*

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Después de iniciar el contenedor, se crean archivos y carpetas de MySQL como auto.cnf, ibdata1, ib_logfile*, y directorios mysql/, performance_schema/, sys/, y la base wordpress/.


### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
```
docker run -d --name mysql --network net-wp -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wp123 -v C:\Users\daena\ejercicio3\db:/var/lib/mysql mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Después de crear el contenedor, la carpeta db se llena automáticamente con los archivos del sistema de bases de datos de MySQL (ibdata1, ib_logfile0, ib_logfile1, carpeta mysql, performance_schema, sys y la base de datos wordpress).
Esto confirma que MySQL está guardando la información del contenedor directamente en el host.


### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wp123 -e WORDPRESS_DB_NAME=wordpress -p 9500:80 -v C:\Users\daena\ejercicio3\www:/var/www/html wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
El sitio web y las publicaciones creadas siguen intactas. Esto ocurre porque los datos del sitio se guardan en la base de datos MySQL (montada en .../ejercicio3/db) y los archivos del sitio (temas, plugins, media) están en .../ejercicio3/www.
Por lo tanto, al eliminar y recrear el contenedor WordPress, la información persiste gracias a los volúmenes montados en el host.
