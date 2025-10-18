# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
docker run -d --name mi_nginx -p 8080:80 -v C:\Users\daena\nginx\html:/usr/share/nginx/html nginx:alpine


### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Se observa una página con el error 403 (forbidden), porque la carpeta /usr/share/nginx/html del contenedor está vacía ya que se reemplazó con la carpeta vacía del host.

### ¿Qué pasa con el archivo index.html del contenedor?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El archivo index.html original del contenedor se oculta o reemplaza temporalmente, porque el bind mount monta la carpeta del host sobre esa ruta (/usr/share/nginx/html).
Es decir, se deja de ver el archivo del contenedor y solo se muestran los archivos de la carpeta del host.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Ahora se muestra el sitio del template descargado, ya que nginx está sirviendo directamente los archivos HTML desde la carpeta html del computador.

### Eliminar el contenedor
# COMPLETAR CON EL COMANDO
docker rm -f mi_nginx


### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El sitio web sigue visible exactamente igual, porque los archivos HTML están almacenados en la carpeta del host. Al eliminar el contenedor, los archivos no se borran, ya que pertenecen al sistema de archivos del host, no al contenedor.

