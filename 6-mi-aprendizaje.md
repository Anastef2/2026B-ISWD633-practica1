# Mi aprendizaje

## Antes de la práctica
Antes de esta práctica ya sabía levantar contenedores con `docker run`, pero no tenía claro qué pasaba con la información. Daba por hecho que si borraba un contenedor se perdía todo, y nunca me había preguntado dónde se guardan realmente los datos de una base de datos o de una página web dentro de Docker.

## Lo que aprendí
Lo más importante fue entender que el contenedor y los datos son cosas separadas. Ahora distingo los tres tipos de montaje: el bind mount, que usa una carpeta de mi propia computadora; el volumen nombrado, que lo administra Docker y se identifica con un nombre; y el volumen anónimo, que Docker crea sin nombre y sirve más para cosas temporales.

Lo que más me ayudó a entenderlo fue probarlo. Con WordPress y MySQL eliminé los contenedores y los volví a crear, y el sitio seguía igual: con el título, el tema y la entrada que había hecho. Ahí entendí de verdad para qué sirven los volúmenes.

También me sorprendió que, al montar la carpeta html vacía en nginx, apareciera un error 403. Al principio pensé que había hecho algo mal, pero era porque la carpeta de mi PC tapaba el index.html que traía el contenedor. Cuando puse el template, la página apareció sin tener que reiniciar nada.

Aprendí que los contenedores que están en la misma red se pueden comunicar usando su nombre, como `server-postgres` o `mysql-wp`, sin necesidad de saber la IP ni de exponer puertos. Y me di cuenta de lo importante que es leer la documentación de cada imagen en Docker Hub, porque ahí dice en qué ruta guarda sus datos cada servicio (por ejemplo `/var/lib/mysql` o `/var/www/html`).

Además, practiqué bastante con Git: hacer un fork, clonar el repositorio y subir mis cambios con add, commit y push.

## Problemas que tuve y cómo los resolví
- Al ejecutar `docker ps` me salió un error de conexión. Era porque Docker Desktop estaba cerrado; lo abrí, esperé a que arrancara y volví a probar.
- pgAdmin y WordPress usaban el mismo puerto (9500), así que tuve que detener WordPress con `docker stop wordpress-wp` antes de crear pgAdmin.
- Al hacer `git push` me lo rechazó porque en GitHub había cambios que no tenía en mi computadora. Lo solucioné trayendo esos cambios con `git pull --no-rebase` y después subiendo de nuevo.
- Git no me dejaba hacer commits porque no tenía configurado mi nombre y correo, así que los agregué con `git config --global`.
- Un par de veces pegué en la terminal los comandos con las comillas ``` del Markdown y me dio error. Aprendí que esas comillas solo son para el documento.

## Otros comandos que usé
- `docker ps -a` para ver todos los contenedores, incluso los que estaban detenidos.
- `docker stop wordpress-wp` para detener un contenedor sin borrarlo.
- `docker rm -f nginx-bind` para eliminar un contenedor aunque estuviera corriendo.
- `git pull --no-rebase` para traer los cambios de GitHub y unirlos con los míos.