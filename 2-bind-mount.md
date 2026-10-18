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
```
docker run -d --name nginx-bind -P -v C:\Users\analu\nginx\html:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Aparece el error 403 Forbidden, porque la carpeta html del host está vacía y nginx no encuentra ningún archivo para mostrar.

### ¿Qué pasa con el archivo index.html del contenedor?
Queda oculto, no se elimina. Al montar la carpeta del host sobre /usr/share/nginx/html, el contenido original se reemplaza por el de la carpeta del host, que está vacía.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Se muestra la página del template descargado. Como la carpeta html del host está montada en /usr/share/nginx/html, nginx ahora encuentra el index.html del template y lo muestra, sin necesidad de reiniciar el contenedor.

### Eliminar el contenedor
```
docker rm -f nginx-bind
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Se sigue mostrando la página del template. Aunque el contenedor anterior se eliminó, los archivos están guardados en la carpeta html del host, por lo que el nuevo contenedor los vuelve a montar y los muestra. Los datos persisten porque no dependen del ciclo de vida del contenedor.


