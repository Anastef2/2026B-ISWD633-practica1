## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: C:\Users\analu\ejercicio3\db

### ¿Qué contiene la carpeta db del host?
Está vacía, porque todavía no se ha creado el contenedor de MySQL.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-wp --network net-wp -v C:\Users\analu\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wp123 mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Ahora contiene los archivos que MySQL generó al iniciar, como archivos del sistema, de configuración y la carpeta de la base de datos "wordpress". Esto pasa porque la carpeta /var/lib/mysql del contenedor está montada en la carpeta db del host.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: C:\Users\analu\ejercicio3\www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name wordpress-wp --network net-wp -p 9500:80 -v C:\Users\analu\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=mysql-wp -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wp123 -e WORDPRESS_DB_NAME=wordpress wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada


### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

La información se mantiene: el sitio conserva el título, la apariencia personalizada y la entrada creada. Aunque los contenedores se eliminaron, los datos de MySQL quedaron guardados en la carpeta db y los archivos de WordPress en la carpeta www del host. Al crear los contenedores nuevamente con los mismos bind mounts, vuelven a leer esa información, por lo que los datos persisten.

